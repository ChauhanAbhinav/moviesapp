<template>
  <div class="moviebox">
    <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path" alt="Movie Poster" />
  </div>
  <div class="moviebox movie-detail">
    <h2>{{movie.title}}</h2>
    <p>{{ movie.release_date }}</p>
    <p>{{ movie.overview }}</p>
  </div>
</template>

<script>
import { ref } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
  setup () {
    const movie = ref({});
    const route = useRoute();


      fetch(`https://api.themoviedb.org/3/movie/${route.params.id}?api_key=${env.apikey}&language=en-US`)
        .then(response => response.json())
        .then(data => {
          console.log(data)
          movie.value = data;
        });
    return {
      movie
    }
  }
}
</script>

<style>
  p {
    color: #000;
    font-size: 18px;
    line-height: 1.4;
  }
    .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }
    h2 {
    color: #42b983;;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }
.movie-detail {
  padding: 16px;
}
.moviebox {
  margin-top: 20px;
  width: 40%;
  display: inline-block;
  line-height: normal;
  vertical-align: middle;
}
</style>