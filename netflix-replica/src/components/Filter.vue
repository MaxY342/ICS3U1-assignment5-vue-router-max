<script setup>
import axios from "axios";
import { ref, onMounted, watch } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const selectedGenres = ref([]);
const selectedYear = ref('');
const minRating = ref(1);
const items = ref([]);
const type = ref('');
const movieGenres = ref([]);
const tvGenres = ref([]);
const genres = ref([]);
const selectedSortBy = ref('');
const sortBy = [
    {name: 'Popularity(asc)', value: 'popularity.asc'},
    {name: 'Popularity(desc)', value: 'popularity.desc'},
    {name: 'Score(asc)', value: 'vote_average.asc'},
    {name: 'Score(desc)', value: 'vote_average.desc'},
    {name: 'Name(asc)', value: 'name.asc'},
    {name: 'Name(desc)', value: 'name.desc'},
];
const voteCount = ref(100);

async function getGenres() {
    const movieResponse = await axios.get(`https://api.themoviedb.org/3/genre/movie/list?api_key=${import.meta.env.VITE_TMDB_KEY}`);
    movieGenres.value = movieResponse.data.genres;

    const tvResponse = await axios.get(`https://api.themoviedb.org/3/genre/tv/list?api_key=${import.meta.env.VITE_TMDB_KEY}`);
    tvGenres.value = tvResponse.data.genres;
}

async function searchItems(type) {
    if (type == 'movie') {
        const query = {
            api_key: import.meta.env.VITE_TMDB_KEY,
            with_genres: selectedGenres.value.join(','),
            sort_by: selectedSortBy.value,
            primary_release_year: selectedYear.value,
            'vote_average.gte': minRating.value,
            'vote_count.gte': voteCount.value,
        };

        const response = await axios.get('https://api.themoviedb.org/3/discover/movie', { params: query });
        items.value = response.data.results;
    }
    else {
        const query = {
            api_key: import.meta.env.VITE_TMDB_KEY,
            with_genres: selectedGenres.value.join(','),
            sort_by: selectedSortBy.value,
            first_air_date_year: selectedYear.value,
            'vote_average.gte': minRating.value,
            'vote_count.gte': voteCount.value,
        };

        const response = await axios.get('https://api.themoviedb.org/3/discover/tv', { params: query });
        items.value = response.data.results;
    }
}

function getMovieDetails(id) {
    router.push(`/movies/${id}`);
}

onMounted(() => {
  getGenres();
});

watch(type, () => {
  genres.value = type.value == 'movie' ? movieGenres.value : tvGenres.value
  selectedGenres.value = []
});
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
                        <option value="" disabled selected>Click to Select</option>
                        <option value="movie">Movie</option>
                        <option value="tv-show">Tv Show</option>
                    </select>
                </div>
                <div class="filter">
                    <div class="filter-name">
                        Sort By
                    </div>
                    <select v-model="selectedSortBy">
                        <option value="" disabled selected>Click to Select</option>
                        <option v-for="option in sortBy" :value="option.value">{{ option.name }}</option>
                    </select>
                </div>
                <div class="filter">
                    <div class="filter-name">
                        Minimum Score
                    </div>
                    <select v-model.number="minRating">
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
                <div class="filter">
                    <div class="filter-name">
                        Minimum vote count
                    </div>
                    <input v-model="voteCount" type="number">
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
                <p class="movie-title">{{ type == 'movie' ? item.title : item.name }}</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .filter-block {
        padding: 100px;
        border-radius: 10px;
        gap: 10px;
        background-color: ;
    }

    .filter {
        float: left;
        margin: 0 10px 10px 0;
        border: 1px solid #e20c0c79;
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