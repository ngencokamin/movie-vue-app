<template>
  <div class="home">
    <h1>Movies</h1>

    <div class="input-group mb-3">
      <div class="input-group-prepend">
        <button
          class="btn btn-outline-secondary dropdown-toggle"
          type="button"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          Sort By
        </button>
        <div class="dropdown-menu">
          <a class="dropdown-item" v-on:click="(sortBy = 'title'), (order = 1)">Name (asc)</a>
          <a class="dropdown-item" v-on:click="(sortBy = 'title'), (order = -1)">Name (desc)</a>
          <a class="dropdown-item" v-on:click="(sortBy = 'year'), (order = 1)">Year (asc)</a>
          <a class="dropdown-item" v-on:click="(sortBy = 'year'), (order = -1)">Year (desc)</a>
        </div>
      </div>
      <input
        type="text"
        class="form-control"
        aria-label="Filter text"
        placeholder="Type to filter..."
        list="titles"
        v-model="filter"
      />
    </div>

    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>

    <div class="row ">
      <div
        class="col-md-5 mx-auto"
        v-for="movie in orderBy(filterBy(movies, filter, 'title'), sortBy, order)"
        :key="movie.id"
      >
        <div class="card mb-3" style="max-width: 800px;">
          <div class="row no-gutters">
            <div class="col-md-4">
              <img :src="movie.poster" class="card-img" alt="Movie poster" />
            </div>
            <div class="col-md-8">
              <div class="card-body">
                <h5 class="card-title">{{ movie.title }}</h5>
                <h6 class="card-text">{{ movie.director }} | {{ movie.year }} | English: {{ movie.english }}</h6>
                <p class="card-text">
                  {{ movie.plot }}
                </p>
                <router-link :to="`/movies/${movie.id}`" custom v-slot="{ navigate }">
                  <span class="btn btn-outline-primary" @click="navigate" @keypress.enter="navigate" role="link">
                    More Info
                  </span>
                </router-link>
              </div>
            </div>
          </div>
        </div>
      </div>
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
      order: 1,
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
