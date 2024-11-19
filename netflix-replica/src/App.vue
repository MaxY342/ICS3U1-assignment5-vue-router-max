<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/Hero.vue'
</script>

<template>
  <Suspense>
    <RouterView />
  </Suspense>
</template>

<style scoped>

</style>
