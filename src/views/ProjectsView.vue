<script setup>
import { ref } from 'vue';
import FilterBar from '@/components/FilterBar.vue';
import VisProject from '@/components/VisProject.vue';

// 1. Create the state variable to hold the selection
const selectedCategory = ref('Vis Project');
</script>

<template>
  <div class="projects-page">
    <h1 class="page-title">My Projects</h1>

    <FilterBar
      v-model="selectedCategory"
      :options="['Vis Project', 'Data Visualization', 'Machine Learning', 'Web Development']"
      label="Filter by category:"
    >
      <template #actions>
        <button class="refresh-btn">Refresh Data</button>
      </template>
    </FilterBar>

    <div class="project-display">
      <p>Showing: <strong>{{ selectedCategory }}</strong></p>
      <VisProject :category="selectedCategory" />
    </div>
  </div>
</template>

<style scoped>
.projects-page {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.page-title {
  text-align: center;
  margin-top: 40px;
  color: #2c3e50;
}

.project-display {
  margin-top: 30px;
}

.project-display p {
  text-align: center;
  font-size: 1.2em;
  color: #34495e;
  margin-bottom: 20px;
}

.refresh-btn {
  background: #f8fafc;
  border: 1px solid #cbd5e1;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
}
</style>