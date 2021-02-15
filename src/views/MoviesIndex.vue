<template>
  <div class="home">
    <h1>Movies</h1>
    <div v-for="movie in movies" :key="movie.id">
      <h2>{{ movie.title }}</h2>
      <p>{{ movie.director }} | {{ movie.year }} | English: {{ movie.english }}</p>
      <p>{{ movie.plot }}</p>
      <p>Genres:</p>
      <div v-for="genre in movie.genres" :key="genre.id">
        <p>
          <b>{{ genre }}</b>
        </p>
      </div>
      <router-link :to="`/movies/${movie.id}`"><button>More Info</button></router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movies: [],
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>
