<script setup>
import VideoList from './components/VideoList.vue'
</script>

<template>
  <header>
    <h1>Lista de Vídeos</h1>
  </header>
  <main>
    <!-- <TheWelcome /> -->
    <VideoList/>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  /* header .wrapper {
    display: flex;
    place-items: start;
    flex-wrap: wrap;
  } */
}
</style>
