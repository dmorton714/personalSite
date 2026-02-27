<script setup>
defineProps({
  centered: {
    type: Boolean,
    default: false
  },
  size: {
    type: String,
    default: "160px"
  }
})
</script>

<template>
  <h1 class="logo" :class="{ centered }">
    <span class="light">danny</span><span class="bold">morton</span>
  </h1>
</template>


<style scoped>
.logo {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: v-bind(size);
  margin: 0;
  line-height: 1;
  opacity: 0;
  animation: fadeIn 0.8s ease forwards;
}

.light {
  font-weight: 300;
  color: #A6A6A6;
}

.bold {
  font-weight: 500;
  color: #5A5A5A;
}

.centered {
  text-align: center;
}

@keyframes fadeIn {
  to {
    opacity: 1;
  }
}
</style>