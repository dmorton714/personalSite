<script setup>
// Expose the base URL to the template
const baseUrl = import.meta.env.BASE_URL;

// Store only the filenames to keep the data clean
const allImages = [
  "3DAB76AB-3CD9-48D1-9EFE-6A22E330529E.jpg", 
  "IMG_4456.jpg",
  "49034C2D-1530-4D04-95C3-00980EF698CE.jpg", 
  "IMG_5066.jpg",
  "5C00BB05-6414-4A7E-9E30-72327B7AA5B1.jpg", 
  "IMG_6641.jpg",
  "FD4D8D4F-877D-4335-9590-80D9904020AB.jpg", 
  "IMG_8750.jpg",
  "IMG_0319.jpg", 
  "IMG_8753.jpg",
  "IMG_4038.jpg", 
  "climb.jpg",
  "IMG_4127.jpg", 
  "ocean.jpg",
  "IMG_4307.jpg", 
  "skate.jpg",
  "IMG_4428.jpg"
];
</script>

<template>
  <div class="gallery-root">
    <div class="honeycomb-wrapper">
      <div class="hex-row">
        <div v-for="img in allImages.slice(0, 6)" :key="img" class="hex-item">
          <div class="unfold-box">
            <img :src="`${baseUrl}about/${img}`" :alt="img" class="hex-img" />
          </div>
        </div>
      </div>

      <div class="hex-row stagger">
        <div v-for="img in allImages.slice(6, 11)" :key="img" class="hex-item">
          <div class="unfold-box">
            <img :src="`${baseUrl}about/${img}`" :alt="img" class="hex-img" />
          </div>
        </div>
      </div>

      <div class="hex-row">
        <div v-for="img in allImages.slice(11, 17)" :key="img" class="hex-item">
          <div class="unfold-box">
            <img :src="`${baseUrl}about/${img}`" :alt="img" class="hex-img" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.gallery-root {
  width: 100%;
  max-width: 90%; 
  margin: 0 auto;
  padding-top: 70px;
  padding-bottom: 150px;
}

.honeycomb-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.hex-row {
  display: flex;
  justify-content: center;
  margin-bottom: -45px; 
}

.hex-item {
  width: 200px;
  height: 220px;
  margin: 0 5px;
  position: relative;
  transition: z-index 0.1s;
}

.unfold-box {
  width: 100%;
  height: 100%;
  transition: all 0.6s cubic-bezier(0.16, 1, 0.3, 1);
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  cursor: pointer;
}

.hex-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.hex-item:hover {
  z-index: 500;
}

.hex-item:hover .unfold-box {
  clip-path: polygon(0% 0%, 100% 0%, 100% 100%, 100% 100%, 0% 100%, 0% 100%);
  transform: scale(2.2);
}

.hex-item:hover .hex-img {
  object-fit: contain;
}

/* --- RESPONSIVE --- */

@media (max-width: 1024px) {
  .hex-item { width: 140px; height: 160px; }
  .hex-row { margin-bottom: -30px; }
}

@media (max-width: 768px) {
  .hex-item { width: 100px; height: 115px; margin: 0 3px; }
  .hex-row { margin-bottom: -24.75px; }
}

@media (max-width: 600px) {
  .gallery-root {
    max-width: 100%;
    padding: 100px 0;
  }
  .hex-item { 
    width: 14vw;
    height: 15.5vw;
    margin: 0 0.5vw; 
  }
  .hex-row { 
    margin-bottom: -2.9vw;
  }
  .hex-item:hover .unfold-box {
    transform: scale(1.8); 
  }
}
</style>