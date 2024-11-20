<script setup>
import Login from '../components/Login.vue'
import Topbar from '../components/Topbar.vue';
</script>

<template>
  <main>
    <Topbar />
    <div class="login">
      <Login />
    </div>
  </main>
</template>

<style scoped>
  .login {
    display: grid;
    justify-content: center;
    align-items: center;
  }
</style>
