<script setup>
import Topbar from '../components/Topbar.vue'
import MovieLists from '../components/MovieLists.vue'
import Search from '../components/Search.vue'
import Footer from '../components/Footer.vue'

</script>

<template>
  <main>
    <Topbar />
    <div class="body">
      <Search />
      <MovieLists />
    </div>
    <Footer />
  </main>
</template>

<style scoped>
  .body {
    display: flex;
    flex-direction: column;
    gap: 4rem;
    background-color: #2f2f2f;
    padding: 4rem;
  }
</style>