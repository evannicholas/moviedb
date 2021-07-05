<template>
  <div class="row">
    <div class="col-12 col-lg-3" v-for="movie in movies" :key="movie.imdbID">
      <MovieThumb :movie="movie"></MovieThumb>
    </div>
  </div>
</template>

<script>
import { api } from "boot/axios";
import MovieThumb from "components/MovieThumb.vue";

export default {
  components: {
    MovieThumb,
  },
  data() {
    return {
      movies: [],
    };
  },
  mounted() {
    api
      .get("https://www.omdbapi.com/?apikey=57edaaef&r=json&s=harry")
      .then((response) => (this.movies = response.data.Search));
  },
};
</script>

<style lang="scss" scoped>
</style>