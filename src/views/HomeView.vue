<template>
  <div class="container-xl">

    <div class="container mt-4">

      <div class="container">
        <form @submit.prevent="SearchMovies()">
          <div class="mb-3">
            <input type="text" placeholder="What are you looking for?" v-model="search" class="form-control" />
            <!---button type="submit" value="Search" class="btn btn-primary">Search</button-->
          </div>
        </form>
      </div>

      <div class="movies-list">
        <div class="card mt-4 py-4 px-2 mb-4 text-center shadow-sm" v-for="movie in movies" :key="movie.imdbID">
          <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
            <div class="product-image">
              <img :src="movie.Poster" alt="Movie Poster" class="img shadow-sm"/>
              <div class="type">{{ movie.Type }}</div>
            </div>
            <div class="detail">
              <p class="year">{{ movie.Year }}</p>
              <h3>{{ movie.Title }}</h3>
            </div>
          </router-link>
        </div>
      </div>
    </div>

  </div>
</template>

<script>

import { ref } from 'vue';
import env from '@/env.js';

export default {
  setup () {
    const search = ref("");
    const movies = ref([]);
    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    }
    return {
      search,
      movies,
      SearchMovies
    }
  }
}
</script>