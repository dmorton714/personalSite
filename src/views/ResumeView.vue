<script setup>
import MyResume from '@/components/MyResume.vue';

</script>

<template>
  <div class="about">
    <MyResume />
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
