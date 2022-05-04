<template>
  <div class="home">
    <h2>Popular Movies</h2>
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.id" class="movie-link">
          <div class="product-image">
            <img :src="'https://image.tmdb.org/t/p/w185' + movie.poster_path" alt="Movie Poster" />
            <div class="type">{{ movie.genre.join(", ") }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.release_date }}</p>
            <h3>{{ movie.title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js'

export default {
  setup () {
    const movies = ref([]);
        fetch(`https://api.themoviedb.org/3/movie/popular?api_key=${env.apikey}`)
          .then(response => response.json())
          .then(data => {
            console.log(data.results)
            movies.value = data.results.map((movie)=>{
              let genre = movie.genre_ids.map((id)=>{
                return env.genres[id];
              })
              movie.genre = genre;
              return movie;
            });

          });
    return {
      movies
    }
  }
}
</script>

<style>
.movies-list{
  padding: 20px;
}
.movie{
  display: inline-flex;
  margin-left: 15px;
  margin-right: 15px;
  margin-top: 15px;
}
</style>