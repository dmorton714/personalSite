<script setup>
const projects = [
  { name: "Silverleaf", image: import.meta.env.BASE_URL + "bestone/sheets.png" },
  { name: "Huntington", image: import.meta.env.BASE_URL + "bestone/sheets.png" },
  { name: "Silverleaf 2", image: import.meta.env.BASE_URL + "bestone/sheets.png" },
  { name: "Huntington 2", image: import.meta.env.BASE_URL + "bestone/sheets.png" },
  { name: "Silverleaf 3", image: import.meta.env.BASE_URL + "bestone/sheets.png" },
  { name: "Huntington 3", image: import.meta.env.BASE_URL + "bestone/sheets.png" },
  { name: "Axsium", image: import.meta.env.BASE_URL + "bestone/sheets.png" },
]
</script>

<template>
  <section id="projects">
    <div
      v-for="(project, index) in projects"
      :key="project.name"
      class="project"
      :style="{ top: `${index * 20}px`, left: `${index * 10}px`, zIndex: projects.length - index, transform: `rotate(${index * 3}deg)` }"
    >
      <img :src="project.image" alt="" />
    </div>
  </section>
</template>

<style scoped>
#projects {
  position: relative;
  height: 700px;
}

.project {
  position: absolute;
  cursor: pointer;
  transition: transform 0.3s ease, top 0.3s ease, left 0.3s ease;
}

.project img {
  display: block;
  height: 450px;
  width: auto;
  border-radius: 4px;
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}
.project:hover img {
  transform: scale(1.05) rotate(0deg);
  z-index: 999;
  box-shadow: 0 20px 40px rgba(0,0,0,0.3);
}
</style>