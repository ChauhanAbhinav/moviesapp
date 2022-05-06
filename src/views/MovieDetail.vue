<template>
      <a-row :gutter="[18, 18]" type="flex" class="movie-detail">
      <a-col :md="6"  class="moviebox">
          <a-card>
            <template #cover>
              <img :src="'https://image.tmdb.org/t/p/w342' + movie.poster_path" alt="Movie Poster" style="width: 100%;" />
            </template>
          </a-card>
      </a-col>
      <a-col :md="16"  class="moviebox">
          <a-card >
            <a-card-meta >
              <template #description>
                <div>
                  <h2>{{movie.title}}</h2>
                  <b>{{ movie.release_date }}</b>
                  <br><br>
                  <p>{{ movie.overview }}</p>
              </div>
              </template>
            </a-card-meta>
          </a-card>
      </a-col>
    </a-row>

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
b, p {
  color: #000;
}
.movie-detail {
  padding: 16px;
  padding-left: 24px;
  padding-right: 24px;
}
.moviebox {
text-align: center
}
</style>