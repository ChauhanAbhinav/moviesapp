<template>
  <div class="home">
    <h2>Popular Movies</h2>
    <div class="movies-list">

    <a-row :gutter="[12, 12]" type="flex">
      <a-col v-for="movie in movies" :key="movie.id" :xs="4"  class="movie">
        <router-link :to="'/movie/' + movie.id">
          <a-card hoverable>
            <template #cover>
             <img :src="'https://image.tmdb.org/t/p/w185' + movie.poster_path" alt="Movie Poster" />
            </template>

            <a-card-meta :title="movie.title">
              <template #description>
                <div class="type">{{ movie.genre.join(", ") }}</div>
                <div>Released on <small>{{ movie.release_date }}</small></div>
              </template>
            </a-card-meta>
          </a-card>
        </router-link>
      </a-col>
    </a-row>
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

</style>