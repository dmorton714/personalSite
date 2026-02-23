<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const props = defineProps({
  title: String,
  problemText: String,
  objectives: Array,
  challengeText: String,
  sections: Array // Array of objects { title, content, image, type }
});

const scrollProgress = ref(0);
const pathLength = 5414.29;

const handleScroll = () => {
  const section = document.getElementById("scroll-section");
  if (!section) return;
  const rect = section.getBoundingClientRect();
  const windowHeight = window.innerHeight;
  const total = rect.height + windowHeight;
  const progress = (windowHeight - rect.top) / total;
  scrollProgress.value = Math.min(Math.max(progress, 0), 1);
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
  const elements = document.querySelectorAll(".box, .scroll-img");
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) entry.target.classList.add("visible");
    });
  }, { threshold: 0.2 });
  elements.forEach(el => observer.observe(el));
});

onUnmounted(() => window.removeEventListener("scroll", handleScroll));
</script>

<template>
  <header class="page-header">
    <h1>{{ title }}</h1>
    <p>{{ problemText }}</p>
    <ul v-if="objectives">
      <li v-for="obj in objectives" :key="obj">{{ obj }}</li>
    </ul>
    <p>{{ challengeText }}</p>
  </header>

  <section id="scroll-section">
    <svg class="line-svg" viewBox="-480 0 2300 2241">
        <path :stroke-dasharray="pathLength" :stroke-dashoffset="pathLength - pathLength * Math.min(scrollProgress * 1.4, 1)" d="M-841 100H584c124 0 225 101 225 225v0c0 124-101 225-225 225h-95a281 281 0 00-281 281v0c0 155 125 281 281 281h442c167 0 304 136 304 304v0c0 168-137 304-304 304H795a439 439 0 00-439 439v82" />
    </svg>

    <div class="container">
      <div class="layout-container">
        <template v-for="(item, index) in sections" :key="index">
          <div :class="['box', `box-${(index % 4) + 1}`]">
            <h3>{{ item.title }}</h3>
            <div v-html="item.content"></div>
            <a v-if="item.link" :href="item.link" class="btn">Find out more</a>
          </div>
          <img v-if="item.image" :src="item.image" :class="['scroll-img', `image-${(index % 3) + 1}`]" />
        </template>
      </div>
    </div>
  </section>
</template>

<style scoped>
body {
  margin: 0;
  font-family: "Montserrat", sans-serif;
  width: 100%;
}

.page-header {
  display: block;
  width: 100%;
  margin: 0 auto;
  padding: 6rem 2rem;
  line-height: 1;
  background: linear-gradient(135deg, #1f4fbf 0%, #173b91 100%);
  color: white;
}

.page-header > * {
  max-width: 900px;
}

.page-header h1 {
  font-size: clamp(3rem, 6vw, 5rem);
  font-weight: 800;
  letter-spacing: -0.02em;
  margin-bottom: 2rem;
  line-height: 1.1;
}

.page-header p {
  font-size: 1.2rem;
  line-height: 1.7;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 1.5rem;
}

.page-header ul {
  margin: 2rem 0;
  padding-left: 1.5rem;
}

.page-header li {
  font-size: 1.15rem;
  margin-bottom: 0.75rem;
  line-height: 1.6;
  position: relative;
}

.page-header li::marker {
  color: #a5c8ff;
}

#scroll-section {
  position: relative;
  min-height: 2700px;
  display: grid;
}

.line-svg {
  grid-row: 1;
  grid-column: 1;
  height: 100%;
  min-width: 300px;
  z-index: 1;
}

.container {
  grid-column: 1;
  grid-row: 1;
  margin: 0 auto;
  width: 100%;
  padding: 0 4rem;
  z-index: 2;
}

h2 {
  color: rgb(0, 0, 0);
  font-size: 62px;
  font-weight: 900;
  text-align: right;
  padding-top: 72px;
}

.layout-container {
  padding-top: 8rem;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 2rem;
}

.box {
  background: white;
  padding: 4rem;
  transform: scale(0.8);
  opacity: 0;
  transition: all 0.6s ease;
}

.box.visible {
  transform: scale(1);
  opacity: 1;
}

.box h3 {
  font-size: 32px;
  margin-bottom: 1rem;
}

.box p {
  font-size: 16px;
  margin-bottom: 1.5rem;
}

img {
  width: 100%;
  opacity: 0;
  transform: scale(0.8);
  transition: all 0.6s ease;
}

img.visible {
  opacity: 1;
  transform: scale(1);
}

.btn {
  background: rgb(32, 91, 173);
  color: white;
  padding: 10px 30px;
  border-radius: 999px;
  text-decoration: none;
  font-weight: bold;
  display: inline-block;
  transition: 0.3s;
}

.btn:hover {
  background: rgb(222, 40, 112);
}

/* Layout positions */
.box-1 {
  grid-column: 3 / span 3;
}

.image-1 {
  grid-column: 1 / span 2;
}

.box-2 {
  grid-column: 2 / span 3;
}

.image-2 {
  grid-column: 6 / span 1;
}

.box-3 {
  grid-column: 3 / span 3;
}

.image-3 {
  grid-column: 1 / span 2;
}

.box-4 {
  grid-column: 1 / span 3;
}

.bottom {
  height: 50vh;
}
</style>