<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

// ==============================
// Constants & State
// ==============================
const CARD_HEIGHT = 250 // Width is now dynamic
const CARD_GAP = 60
const MIN_VELOCITY = 60
const DEFAULT_VELOCITY = 120

// Vue Refs for DOM elements and data
const containerRef = ref(null)
const cardLineRef = ref(null)
const cardRefs = ref([])
const cards = ref([])

// Standard variables for the animation loop
let position = 0
let velocity = DEFAULT_VELOCITY
let direction = 1
let isDragging = false
let lastTime = 0
let lastMouseX = 0
let mouseVelocity = 0
let friction = 0.95
let containerWidth = 0
let cardLineWidth = 0
let animationFrameId = null
let intervalId = null
let resizeObserver = null

// ==============================
// Utility Functions
// ==============================
const randInt = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min
const pick = (arr) => arr[randInt(0, arr.length - 1)]

const images = [
  "/scannerImages/balt_trackersm.jpg",
  "/scannerImages/jobboard.jpg",
  "/scannerImages/slsteamsm.jpg",
  "/scannerImages/staatysm.jpg",
  "/scannerImages/tpm.png",
  "/scannerImages/staatysm.jpg",
  
]

const calculateCodeDimensions = () => ({
  width: Math.floor(1000 / 6),
  height: Math.floor(CARD_HEIGHT / 13),
  fontSize: 11,
  lineHeight: 13,
})

const generateCode = (width, height) => {
  const segments = []
  const blocks = [
    "// compiled preview • scanner demo",
    "function clamp(n,a,b){return Math.max(a,Math.min(b,n));}",
    "const SCAN_WIDTH=8; const FADE_ZONE=35;",
    "const MAX_PARTICLES=2500; const TRANSITION=0.05;"
  ]

  for (let i = 0; i < 40; i++) {
    segments.push(`const v${i}=(${randInt(1, 9)}+${randInt(10, 99)})*0.${randInt(1, 9)};`)
  }

  let flow = blocks.concat(segments).join(" ").replace(/\s+/g, " ").trim()
  const totalChars = width * height
  while (flow.length < totalChars + width) {
    flow += " " + pick(blocks)
  }

  let out = ""
  for (let i = 0; i < height; i++) {
    const line = flow.slice(i * width, (i + 1) * width)
    out += line.padEnd(width, " ") + (i < height - 1 ? "\n" : "")
  }
  return out
}

const populateCards = () => {
  const { width, height } = calculateCodeDimensions()
  for (let i = 0; i < 30; i++) {
    cards.value.push({
      id: i,
      image: images[i % images.length],
      ascii: generateCode(width, height)
    })
  }
}

// ==============================
// Animation & Physics Logic
// ==============================
const recalculateDimensions = () => {
  if (!containerRef.value || !cardLineRef.value) return
  containerWidth = containerRef.value.offsetWidth
  // Dynamically measure the true scrollable width of the entire row of cards
  cardLineWidth = cardLineRef.value.scrollWidth
}

const updateTransform = () => {
  if (cardLineRef.value) {
    cardLineRef.value.style.transform = `translateX(${position}px)`
  }
}

const updateCardClipping = () => {
  if (!containerRef.value) return

  const containerRect = containerRef.value.getBoundingClientRect()
  const scannerX = containerRect.left + (containerRect.width / 2)
  const scannerWidth = 8
  const left = scannerX - scannerWidth / 2
  const right = scannerX + scannerWidth / 2

  cardRefs.value.forEach((wrapper) => {
    if (!wrapper) return
    const rect = wrapper.getBoundingClientRect()
    const { left: cardLeft, right: cardRight, width: cardWidth } = rect
    const normal = wrapper.querySelector(".card-normal")
    const ascii = wrapper.querySelector(".card-ascii")

    const intersects = cardLeft < right && cardRight > left
    if (intersects) {
      const leftPx = Math.max(left - cardLeft, 0)
      const rightPx = Math.min(right - cardLeft, cardWidth)

      normal.style.setProperty("--clip-right", `${(leftPx / cardWidth) * 100}%`)
      ascii.style.setProperty("--clip-left", `${(rightPx / cardWidth) * 100}%`)

      if (!wrapper.hasAttribute("data-scanned") && leftPx > 0) {
        wrapper.setAttribute("data-scanned", "true")

        const scan = document.createElement("div")
        scan.className = "scan-effect"
        wrapper.appendChild(scan)
        setTimeout(() => scan.remove(), 600)
      }
    } else {
      normal.style.setProperty("--clip-right", cardRight < left ? "100%" : "0%")
      ascii.style.setProperty("--clip-left", cardLeft > right ? "0%" : "100%")
      wrapper.removeAttribute("data-scanned")
    }
  })
}

const animate = (time) => {
  const dt = (time - lastTime) / 1000
  lastTime = time

  // Only run physics if the user isn't actively dragging
  if (!isDragging) {
    velocity = Math.max(MIN_VELOCITY, velocity * friction)
    position += velocity * direction * dt

    if (position < -cardLineWidth) position = containerWidth
    else if (position > containerWidth) position = -cardLineWidth

    updateTransform()
    updateCardClipping()
  }

  animationFrameId = requestAnimationFrame(animate)
}

// ==============================
// Event Handlers
// ==============================
const startDrag = (e) => {
  isDragging = true
  lastMouseX = e.clientX || e.touches?.[0].clientX
  mouseVelocity = 0

  if (cardLineRef.value) {
    cardLineRef.value.classList.add("dragging")
  }
  document.body.style.userSelect = "none"
  document.body.style.cursor = "grabbing"
}

const onDrag = (e) => {
  if (!isDragging) return
  const currentX = e.clientX || e.touches?.[0].clientX
  const deltaX = currentX - lastMouseX
  position += deltaX
  mouseVelocity = deltaX * 60
  lastMouseX = currentX

  updateTransform()
  updateCardClipping()
}

const endDrag = () => {
  if (!isDragging) return
  isDragging = false

  if (cardLineRef.value) {
    cardLineRef.value.classList.remove("dragging")
  }
  document.body.style.userSelect = ""
  document.body.style.cursor = ""

  const absVel = Math.abs(mouseVelocity)
  velocity = absVel > MIN_VELOCITY ? absVel : DEFAULT_VELOCITY
  direction = mouseVelocity > 0 ? 1 : -1
}

const onWheel = (e) => {
  e.preventDefault()
  position += e.deltaY > 0 ? 20 : -20
  updateTransform()
  updateCardClipping()
}

// ==============================
// Lifecycle Hooks
// ==============================
onMounted(() => {
  populateCards()

  setTimeout(() => {
    recalculateDimensions()
    position = containerWidth / 2 - cardLineWidth / 2
    lastTime = performance.now()
    animationFrameId = requestAnimationFrame(animate)

    // Watch for image load events to dynamically adjust the loop length
    if (cardLineRef.value) {
      resizeObserver = new ResizeObserver(() => recalculateDimensions())
      resizeObserver.observe(cardLineRef.value)
    }

    window.addEventListener("resize", recalculateDimensions)
    document.addEventListener("mousemove", onDrag)
    document.addEventListener("mouseup", endDrag)
    document.addEventListener("touchmove", onDrag, { passive: false })
    document.addEventListener("touchend", endDrag)
  }, 0)

  intervalId = setInterval(() => {
    const { width, height } = calculateCodeDimensions()
    cards.value.forEach((card) => {
      if (Math.random() < 0.15) card.ascii = generateCode(width, height)
    })
  }, 200)
})

onBeforeUnmount(() => {
  cancelAnimationFrame(animationFrameId)
  clearInterval(intervalId)
  if (resizeObserver) resizeObserver.disconnect()
  window.removeEventListener("resize", recalculateDimensions)
  document.removeEventListener("mousemove", onDrag)
  document.removeEventListener("mouseup", endDrag)
  document.removeEventListener("touchmove", onDrag)
  document.removeEventListener("touchend", endDrag)
})
</script>

<template>
  <div class="home-hero">
    <div class="container" ref="containerRef">
      <div class="card-stream">
        <div
          class="card-line"
          ref="cardLineRef"
          @mousedown.prevent="startDrag"
          @touchstart.prevent="startDrag"
          @wheel.prevent="onWheel"
          @selectstart.prevent
          @dragstart.prevent
        >
          <div
            v-for="(card, index) in cards"
            :key="card.id"
            class="card-wrapper"
            :ref="el => cardRefs[index] = el"
          >
            <div class="card card-normal">
              <img :src="card.image" class="card-image" alt="Scanner Graphic" />
            </div>

            <div class="card card-ascii">
              <div class="ascii-content" v-text="card.ascii"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.home-hero {
  position: relative;
  width: 100% !important;
  height: 350px;
  overflow: hidden;
  margin: 20px auto;
}

.container {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-stream {
  position: absolute;
  width: 100%;
  height: 180px;
  display: flex;
  align-items: center;
  overflow: visible;
}

.card-line {
  display: flex;
  align-items: center;
  gap: 60px;
  white-space: nowrap;
  cursor: grab;
  user-select: none;
  will-change: transform;
}

.card-line:active, .card-line.dragging {
  cursor: grabbing;
}

/* Wrapper now uses flex to snap to the width of the image inside it */
.card-wrapper {
  position: relative;
  height: 250px;
  flex-shrink: 0;
  display: flex;
}

/* We removed the .card class that forced the 400px width */

.card-normal {
  background: transparent;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.4);
  z-index: 2;
  position: relative; /* Drives the width of the wrapper */
  height: 100%;
  border-radius: 15px;
  overflow: hidden;
  clip-path: inset(0 0 0 var(--clip-right, 0%));
}

.card-image {
  height: 100%;
  width: auto;
  display: block;
  transition: all 0.3s ease;
  filter: brightness(1.1) contrast(1.1);
}

.card-image:hover {
  filter: brightness(1.2) contrast(1.2);
}

.card-ascii {
  background: transparent;
  z-index: 1;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 15px;
  overflow: hidden;
  clip-path: inset(0 calc(100% - var(--clip-left, 0%)) 0 0);
}

.ascii-content {
  position: absolute;
  top: 0;
  left: 0;
  width: 1000px;
  height: 100%;
  color: rgb(0, 0, 0);
  font-family: "Courier New", monospace;
  font-size: 11px;
  line-height: 13px;
  overflow: hidden;
  white-space: pre;
  animation: glitch 0.1s infinite linear alternate-reverse;
  -webkit-mask-image: linear-gradient(to right, rgba(0,0,0,1) 0%, rgba(0,0,0,0.8) 30%, rgba(0,0,0,0.6) 50%, rgba(0,0,0,0.4) 80%, rgba(0,0,0,0.2) 100%);
  mask-image: linear-gradient(to right, rgba(0,0,0,1) 0%, rgba(0,0,0,0.8) 30%, rgba(0,0,0,0.6) 50%, rgba(0,0,0,0.4) 80%, rgba(0,0,0,0.2) 100%);
}

:deep(.scan-effect) {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(0, 255, 255, 0.4), transparent);
  animation: scanEffect 0.6s ease-out;
  pointer-events: none;
  z-index: 5;
}

@keyframes scanEffect {
  0% { transform: translateX(-100%); opacity: 0; }
  50% { opacity: 1; }
  100% { transform: translateX(100%); opacity: 0; }
}
</style>
