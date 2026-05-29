<script setup>
import { ref } from 'vue';
import FilterBar from '@/components/FilterBar.vue';
import StaatyProject from '@/components/projects/StaatyProject.vue';
import PropProject from '@/components/projects/PropProject.vue';
import VisProject from '@/components/projects/VisProject.vue';
import DataPipeline from '@/components/projects/DataPipeline.vue';
import JobBoard from '@/components/projects/JobBoard.vue';
import OtherProjects from '@/components/projects/OtherProjects.vue';

// 1. Create the state variable to hold the selection
const selectedCategory = ref('STAATY');
</script>

<template>
  <div class="projects-page">
    <h1 class="page-title">My Projects</h1>

    <FilterBar v-model="selectedCategory"
      :options="['STAATY', 'PropMG', 'Vis', 'Data Pipeline', 'Job Board', 'Other Projects']" label="Filter by Project:" />

    <div class="project-display">

      <StaatyProject v-if="selectedCategory === 'STAATY'" />

      <PropProject v-if="selectedCategory === 'PropMG'" />

      <VisProject v-if="selectedCategory === 'Vis'" />

      <DataPipeline v-else-if="selectedCategory === 'Data Pipeline'" />

      <JobBoard v-else-if="selectedCategory === 'Job Board'" />

      <OtherProjects v-else-if="selectedCategory === 'Other Projects'" />
    </div>
  </div>
</template>

<style scoped>
.projects-page {
  width: 100%;
  padding: 0;
}

.page-title {
  text-align: center;
  margin-top: 10px;
  padding: 0 20px;
  color: #2c3e50;
}

.project-display {
  margin-top: 10px;
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