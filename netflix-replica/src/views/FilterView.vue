<script setup>
import Topbar from '../components/Topbar.vue'
import Filter from '../components/Filter.vue'

</script>

<template>
  <main>
    <Topbar />
    <div class="filter-container">
      <Filter />
    </div>
  </main>
</template>

<style scoped>
  .filter-container {
    background-color: #2f2f2f;
    padding-top: 4rem;
  }
</style>