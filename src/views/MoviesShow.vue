<template>
  <div class="home">
    <h1>Movies</h1>
    <h2>{{ movie.title }}</h2>
    <p>{{ movie.director }} | {{ movie.year }} | English: {{ movie.english }}</p>
    <p>{{ movie.plot }}</p>
    <p>Genres:</p>
    <div v-for="genre in movie.genres" :key="genre.id">
      <p>
        <b>{{ genre }}</b>
      </p>
    </div>
    <router-link to="/movies"><button>Back</button></router-link>
    <router-link :to="`/movies/${this.movie.id}/edit`"><button>Edit Movie</button></router-link>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movie: {},
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {},
};
</script>
