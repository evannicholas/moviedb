<template>
  <div>
    <div class="row" v-if="movie != null">
      <div class="col-6 col-lg-3 q-pa-lg">
        <q-img
          :src="movie.Poster"
          :ratio="0.69"
          spinner-color="primary"
          spinner-size="82px"
        />
      </div>
      <div class="col-6 col-lg-9 q-pa-lg">
        <div class="title">{{ movie.Title }} ({{ movie.Year }})</div>
        <div class="detail">
          <span class="highlight">Director:</span> {{ movie.Director }}
        </div>
        <div class="detail">
          <span class="highlight">Actors:</span> {{ movie.Actors }}
        </div>
        <div class="detail">
          <span class="highlight">Awards:</span> {{ movie.Awards }}
        </div>
        <div class="detail">
          <span class="highlight">Plot:</span> {{ movie.Plot }}
        </div>
        <div class="detail q-mt-md">
          <q-btn
            type="a"
            :href="`http://imdb.com/title/${$route.params.imdbID}`"
            target="_blank"
            icon="description"
            label="IMDB"
            color="secondary"
          />
        </div>
      </div>
    </div>
    <div v-else class="loading">
      <!-- <q-spinner-gears color="primary" size="3rem" :thickness="5" /> -->
      <q-spinner-pie color="primary" size="100px" />
    </div>
  </div>
</template>

<script>
import { api } from "boot/axios";
export default {
  data() {
    return {
      movie: null,
    };
  },
  mounted() {
    api
      .get(
        `https://www.omdbapi.com/?apikey=57edaaef&r=json&i=+${this.$route.params.imdbID}`
      )
      .then((response) => (this.movie = response.data));
  },
};
</script>

<style lang="scss" scoped>
.title {
  font-size: 25px;
  color: $primary;
}
.detail {
}
.highlight {
  color: $secondary;
}
.loading {
  padding-top: 300px;
  text-align: center;
}
</style>