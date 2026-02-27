<script setup>
import DataToImages from '@/components/DataToImages.vue';
import DmLogo from '@/components/DmLogo.vue';
</script>

<template>
  <main>
    <DmLogo :centered="true" size="clamp(50px, 10vw, 120px)" />
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

main {
  width: 100%;
  overflow-x: hidden; 
  padding: 40px 20px;
  box-sizing: border-box;
}

.bio {
  max-width: 600px;
  margin: 20px auto 40px auto;
  font-size: 1.2rem;
  line-height: 1.6;
  color: #333;
  text-align: center;
}

/* RESPONSIVE / MOBILE */
@media (max-width: 768px) {
  main {
    padding: 20px 15px;
  }

  .bio {
    font-size: 1.05rem;
    margin: 15px auto 30px auto; 
  }
}
</style>
