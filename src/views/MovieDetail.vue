<template>
    <div class="container-xl mt-4">
        <div class="movie-detail">
            <img :src="movie.Poster" alt="Movie Poster" class="img-fluid shadow-sm" />
            <div class="card mt-2 px-4 py-4 mb-2 shadow-sm">
                <h2>{{movie.Title}}</h2>
                <h3 class="text-muted">{{ movie.Year }}</h3>
                <p class="mt-2">{{ movie.Plot }}</p>
            </div>
        </div>
    </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';
export default {
  setup () {
    const movie = ref({});
    const route = useRoute();
    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
          movie.value = data;
        });
    });
    return {
      movie
    }
  }
}
</script>

<style>



</style>