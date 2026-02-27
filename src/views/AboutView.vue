<script setup>
import PhotoGrid from '@/components/about/PhotoGrid.vue';


</script>

<template>
  <div class="about">
    <h2 class="about-title">Beyond the Work</h2>

    <p class="lead">
      Most of what you’ll see on this site is the work.<br />
      <span class="highlight">This is the part that’s me.</span>
    </p>

    <p>
      I’ve been lucky enough to be internationally published as a photographer and
      win a few awards along the way. I’ve spent years skateboarding and competing, 
      climbing rocks for fun, riding motorcycles, and hopping on planes whenever I 
      can.
    </p>
    <br>
    <p>
      I’m a Kentucky Colonel and I’ve been given a key to the city of Louisville,
      which still feels surreal. I’m just someone who likes to 
      <span class="emphasis">move, explore, build things, and help people when I can.</span>
    </p>
    <p class="closing">
      At the core, I’m curious and adventurous. I like understanding how things work,
      whether its a camera, internals of my motorcycle, figuring out complex lines on 
      the wall, or code behind an application.
      <br /><br />
      <span class="highlight">That curiosity shows up in everything I do.</span>
    </p>
  </div>
  <div class="phot-grid">
    <PhotoGrid />
  </div>
</template>

<style>
.about {
  max-width: 750px;
  display: block;
  width: 100%;
  margin: 10px auto;
  padding: 0 20px;
  line-height: 1.8;
  font-size: 1.05rem;
}

.about-title {
  font-size: 2rem;
  margin-bottom: 30px;
  font-weight: 600;
}

.lead {
  font-size: 1.2rem;
  margin-bottom: 30px;
}

.highlight {
  font-weight: 600;
}

.emphasis {
  font-weight: 600;
  letter-spacing: 0.5px;
}

.closing {
  margin-top: 40px;
  font-size: 1.1rem;
}

</style>
