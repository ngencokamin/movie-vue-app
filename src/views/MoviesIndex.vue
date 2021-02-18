<template>
  <div class="home">
    <h1>Movies</h1>
    <input v-model="filter" placeholder="Type to filter..." list="titles" />
    <button v-on:click="(sortBy = 'title'), (order = !order)">Sort Alphabetically</button>
    <button v-on:click="(sortBy = 'year'), (order = !order)">Sort By Year</button>
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    <div v-for="movie in orderBy(filterBy(movies, filter, 'title'), sortBy, ascOrDesc())" :key="movie.id">
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
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      filter: "",
      sortBy: "",
      order: false,
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {
    ascOrDesc: function() {
      if (this.order === true) {
        return 1;
      } 
      else {
        return -1;
      }
    },
  },
};
</script>
