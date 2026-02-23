<script setup>
import { ref } from 'vue';
import FilterBar from '@/components/FilterBar.vue';
import VisProject from '@/components/VisProject.vue';
import DataPipeline from '@/components/DataPipeline.vue';
import JobBoard from '@/components/JobBoard.vue';

// 1. Create the state variable to hold the selection
const selectedCategory = ref('Vis Project');
</script>

<template>
  <div class="projects-page">
    <h1 class="page-title">My Projects</h1>

    <FilterBar
      v-model="selectedCategory"
      :options="['Vis Project', 'Data Pipeline Project', 'Job Board', 'Web Development']"
      label="Filter by category:"
    />

    <div class="project-display">
      <p>Showing: <strong>{{ selectedCategory }}</strong></p>

      <VisProject 
        v-if="selectedCategory === 'Vis Project'" 
        :category="selectedCategory" 
      />

      <DataPipeline 
        v-else-if="selectedCategory === 'Data Pipeline Project'" 
        :category="selectedCategory" 
      />

      <JobBoard 
        v-else-if="selectedCategory === 'Job Board'" 
        :category="selectedCategory" 
      />
      
      <div v-else>
        <p>Project details for {{ selectedCategory }} coming soon...</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.projects-page {
  max-width: 90%;
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