<script setup>
import axios from "axios";
import { useRouter } from "vue-router";

const router = useRouter();
const nowPlaying = await axios.get(`https://api.themoviedb.org/3/movie/now_playing?api_key=${import.meta.env.VITE_TMDB_KEY}`);
const trending = await axios.get(`https://api.themoviedb.org/3/trending/all/day?api_key=${import.meta.env.VITE_TMDB_KEY}`)
const topRated = await axios.get(`https://api.themoviedb.org/3/movie/top_rated?api_key=${import.meta.env.VITE_TMDB_KEY}`)
const upcoming = await axios.get(`https://api.themoviedb.org/3/movie/upcoming?api_key=${import.meta.env.VITE_TMDB_KEY}`)

function getMovieDetails(id) {
    router.push(`/movies/${id}`)
}
</script>

<template>
  <div class="movie-gallery">
    <h1>Now Playing</h1>
    <div class="movie-list">
      <div v-for="movie in nowPlaying.data.results.slice(0, 5)" :key="movie.id" class="movie-card" @click="getMovieDetails(movie.id)">
        <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" alt="Movie Poster" class="movie-poster" />
        <p class="movie-title">{{ movie.title }}</p>
      </div>
    </div>
    <button>Veiw More</button>
    <hr style="width:100%">
    <h1>Trending</h1>
    <div class="movie-list">
      <div v-for="item in trending.data.results.slice(0, 5)" :key="item.id" class="movie-card" @click="getMovieDetails(item.id)">
        <img :src="`https://image.tmdb.org/t/p/w500${item.poster_path}`" alt="Movie Poster" class="movie-poster" />
        <p class="movie-title">{{ item.media_type === 'tv' ? item.name : item.title }}</p>
      </div>
    </div>
    <button>Veiw More</button>
    <hr style="width:100%">
    <h1>Top Rated</h1>
    <div class="movie-list">
      <div v-for="movie in topRated.data.results.slice(0, 5)" :key="movie.id" class="movie-card" @click="getMovieDetails(movie.id)">
        <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" alt="Movie Poster" class="movie-poster" />
        <p class="movie-title">{{ movie.title }}</p>
      </div>
    </div>
    <button>Veiw More</button>
    <hr style="width:100%">
    <h1>Upcoming</h1>
    <div class="movie-list">
      <div v-for="movie in upcoming.data.results.slice(0, 5)" :key="movie.id" class="movie-card" @click="getMovieDetails(movie.id)">
        <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" alt="Movie Poster" class="movie-poster" />
        <p class="movie-title">{{ movie.title }}</p>
      </div>
    </div>
    <button>Veiw More</button>

  </div>
</template>

<style scoped>
  h1 {
    text-align: center;
    margin-bottom: 20px;
    font-size: 2.5rem;
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