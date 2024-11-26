<script setup>
import axios from "axios";
import { useRouter } from "vue-router";

const router = useRouter();

function getMovieDetails(id) {
    router.push(`/movies/${id}`)
}

function goToFilter() {
  router.push(`/filter`)
}
</script>

<template>
  <div class="search-section">
    <h1>Search Movie</h1>
    <div class="search-bar">
      <input>
      <button @click="goToFilter">Filter</button>
      <button>Search!</button>
    </div>
  </div>
</template>

<style scoped>
  .search-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    color: white;
  }

  h1 {
    margin-bottom: 20px;
    font-size: 2.5rem;
  }

  .search-bar {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    gap: 20px;
  }

  input {
    height: 2rem;
    width: 70vw;
  }

  button {
    background-color: #e20c0c;
    padding: 1rem;
    margin-top: 50px;
    color: white;
    border: 0;
    border-radius: 10px;
    margin-bottom: 50px;
    transition: transform 0.2s;
  }

  button:hover {
    background-color: #c20000;
    cursor: pointer;
  }
</style>