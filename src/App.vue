<script setup lang="ts">
import NavBar from './components/NavBar.vue';
import HeroSection from './components/HeroSection.vue';
import GsapTest from './components/GsapTest.vue';
</script>

<template>

  <header>
    <NavBar></NavBar>
  </header>

  <main>
    <section class="full-height">
      <hero-section />
    </section>
    <section class="journey-section">
      <gsap-test />
    </section>
    <section class="journey-section">
    </section>
  </main>
</template>

<style scoped>
header {
  width: 100%;
  height: fit-content;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
  padding: 0 2rem;
}

/* Add this line */
main {
  display: flex;
  flex-direction: column;
  height: fit-content;
  padding: 64px 0 0 0;
  /* top and bottom 64px, left and right 0 */
}

.full-height {
  width: 100%;
  height: calc(100vh - 64px);
}

.journey-section {
  width: 100%;
}

@media (min-width: 1024px) {}
</style>
