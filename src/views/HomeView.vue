<script setup>
import DataToImages from '@/components/DataToImages.vue';
import DmLogo from '@/components/DmLogo.vue';
</script>

<template>
  <main>
    <DmLogo :centered="true" size="120px" />
    <p class="bio">
      Turning data and ideas into meaningful experiences is what I love to do.
      I’m passionate about using technology to tackle complex problems and
      create real impact. With a background in design, software development,
      and project management, I enjoy building solutions that not only work
      efficiently but also feel intuitive and engaging for users.
    </p>
    <DataToImages />
  </main>
</template>

<style scoped>
.bio {
  max-width: 600px;
  margin: 20px auto;
  font-size: 1.2em;
  line-height: 1.5;
  color: #333;
}
</style>
