<script setup>
import axios from "axios";
import { ref, computed, onMounted, watch } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const selectedGenres = ref([]);
const selectedYear = ref('');
const minRating = ref(1);
const items = ref([]);
const sortBy = ref('');
const type = ref('movie');
const movieGenres = ref([]);
const tvGenres = ref([]);
const genres = computed(() => type == 'movie' ? movieGenres.value : tvGenres.value);

async function getGenres() {
    const movieResponse = await axios.get(`https://api.themoviedb.org/3/genre/movie/list?api_key=${import.meta.env.VITE_TMDB_KEY}`);
    movieGenres = movieResponse.data.genres;

    const tvResponse = await axios.get(`https://api.themoviedb.org/3/genre/tv/list?api_key=${import.meta.env.VITE_TMDB_KEY}`);
    tvGenres = movieResponse.data.genres;
};

onMounted(() => {
  getGenres();
});

watch(type, () => {
  getGenres();
});

async function searchItems(type) {
    if (type == 'movie') {
        const query = {
            api_key: import.meta.env.VITE_TMDB_KEY,
            with_genres: selectedGenres.value.join(','),
            sort_by: 'popularity.desc',
            primary_release_year: selectedYear.value,
            vote_average: minRating.value,
            language: 'en-US',
        };

        const response = await axios.get('https://api.themoviedb.org/3/discover/movie', { params: query });
        items.value = response.data.results;
    }
    else {
        const query = {
            api_key: import.meta.env.VITE_TMDB_KEY,
            with_genres: selectedGenres.value.join(','),
            sort_by: 'popularity.desc',
            primary_release_year: selectedYear.value,
            vote_average: minRating.value,
            language: 'en-US',
        };

        const response = await axios.get('https://api.themoviedb.org/3/discover/tv', { params: query });
        items.value = response.data.results;
    }
};

function getMovieDetails(id) {
    router.push(`/movies/${id}`);
};
</script>

<template>
    <h1>Filter</h1>
    <div class="filter-block">
        <form @submit.prevent="searchItems(type)">
            <div class="filters">
                <div class="filter">
                    <div class="filter-name">
                        Type
                    </div>
                    <select v-model="type">
                        <option>Movie</option>
                        <option>Tv Show</option>
                    </select>
                </div>
                <div class="filter">
                    <div class="filter-name">
                        Sort By
                    </div>
                    <select v-model="sortBy">
                        <option>Most Watched</option>
                        <option>Score</option>
                        <option>Latest</option>
                        <option>Name</option>
                    </select>
                </div>
                <div class="filter">
                    <div class="filter-name">
                        Minimum Score
                    </div>
                    <select v-model="minRating">
                        <option>1</option>
                        <option>2</option>
                        <option>3</option>
                        <option>4</option>
                        <option>5</option>
                        <option>6</option>
                        <option>7</option>
                        <option>8</option>
                        <option>9</option>
                        <option>10</option>
                    </select>
                </div>
                <div class="filter">
                    <div class="filter-name">
                        Year
                    </div>
                    <input v-model="selectedYear" type="number">
                </div>
            </div>
            <div class="filter genre-select">
                <div class="filter-name">
                    Genre
                </div>
                <div class="checkbox-group">
                    <div v-for="genre in genres" class="checkbox-item">
                        <input type="checkbox" :value="genre.id" v-model="selectedGenres"/>
                        <label>{{ genre.name }}</label>
                    </div>
                </div>
            </div>
            <button type="submit">Filter</button>
        </form>
    </div>
    <div class="filter-results">
        <h1>Filter Results</h1>
        <div class="movie-list">
            <div v-for="item in items" :key="item.id" class="movie-card" @click="getMovieDetails(item.id)">
                <img :src="`https://image.tmdb.org/t/p/w500${item.poster_path}`" alt="Movie Poster" class="movie-poster" />
                <p class="movie-title">{{ item.media_type == 'tv' ? item.name : item.title }}</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .filter-block {

        padding: 100px;
        border-radius: 10px;
        box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
        gap: 10px;
    }

    .filter {
        float: left;
        margin: 0 10px 10px 0;
        border: 1px solid #575a64;
        border-radius: 6px;
        padding: 3px 10px;
    }

    .filter-name {
        font-weight: 500;
        margin-right: 5px;
        float: left;
    }

    .genre-select {
        color: white;

    }

    input {
        height: 1rem;
        width: 50px;
        border-radius: 5px;
        border:none;
        color: #e20c0c;
    }
    
    h1 {
       color:white;
       text-align: center;
    }

    button {
        margin-top: 50px;
        background-color: #e20c0c;
        padding: 1rem;
        color: white;
        border: 0;
        border-radius: 10px;
    }

    button:hover {
        background-color: #c20000;
        cursor: pointer;
    }

    select {
        background-color: #151515;
        color: #e20c0c;
        cursor: pointer;
        border: none;
        padding: 0 5px;
        appearance: none;
    }

    select:focus {
        outline: none;
        border: none;
    }

    .filters {
        color: white;
        display: grid;
        grid-template-columns: auto auto auto;
    }

    .checkbox-group {
        display: flex;
        flex-wrap: wrap;
        gap: 10px;
    }

    .checkbox-item {
        display: flex;
        align-items: center;
    }

    input[type="checkbox"] {
        margin-right: 5px;
    }

    label {
        color: white;
    }

    h1 {
        text-align: center;
        margin-bottom: 20px;
        font-size: 2.5rem;
    }
</style>