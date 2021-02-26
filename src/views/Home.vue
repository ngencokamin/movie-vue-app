<template>
  <div class="home">
    <div class="jumbotron">
      <h1 class="display-4">Oops!</h1>
      <p class="lead">
        Seems there's no data here. Nothing at all.
      </p>
      <hr class="my-4" />
      <p>If you want to see movie data, have you considered checking out our movies index?</p>
      <router-link to="/movies" custom v-slot="{ navigate }">
        <span class="btn btn-primary btn-lg" @click="navigate" @keypress.enter="navigate" role="link">
          Movies Index
        </span>
      </router-link>
    </div>
  </div>
</template>

<style></style>

<script>
export default {
  data: function() {
    return {};
  },
  created: function() {},
  methods: {},
};
</script>
