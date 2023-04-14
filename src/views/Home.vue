<template>
  <base-header />
  <overlay v-if="loading" />
  <div v-else>
    <hero :showlearnmore="true" :movies="movies" />
    <more-movies :movies="movies" />
  </div>
  <base-footer />
</template>

<script setup>
import BaseFooter from "../components/BaseFooter.vue";
import BaseHeader from "../components/BaseHeader.vue";
import Hero from "../components/Hero.vue";
import MoreMovies from "../components/MoreMovies.vue";
import axios from "axios";
import { ref, onMounted } from "vue";
import Overlay from "../components/Overlay.vue";

components: {
  BaseHeader, Hero, MoreMovies, BaseFooter, Overlay;
}

const movies = ref([]);
const loading = ref(true);
const getMovies = async () => {
  await axios
    .get(
      "https://api.themoviedb.org/4/list/4?api_key=5035e33b7502ccacbf835c91b3097af3"
    )
    .then((response) => {
      movies.value = response.data.results;
      loading.value = false;
    });
};

onMounted(() => {
  getMovies();
});
</script>

<style>
</style>