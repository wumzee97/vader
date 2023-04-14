<template>
  <base-header />
  <overlay v-if="loading" />
  <details-hero :movie="movie" :video="videos.key" v-else />
  <div class="hidden lg:block">
    <casts :casts="casts" />
    <more-movies :title="'You might also like'" :movies="similarMovies" />
  </div>
  <div class="lg:hidden py-8 px-4 bg-[#1B1F32]">
    <div class="flex">
      <div @click="tabItem = 'cast'" class=" ">
        <p class="text-[15px] px-4" :class="tabItem == 'cast' ? 'text-[#FDFDFD]' : 'text-[#c3c5ca]'">Cast</p>
        <div v-if="tabItem == 'cast'" class="h-[3px] mt-2 rounded-t-full bg-[#98B6FF]"></div>
      </div>
      <div @click="tabItem = 'recommended'" class="px-2 ml-2">
        <p class="text-[15px] px-4" :class="tabItem == 'recommended' ? 'text-[#FDFDFD]' : 'text-[#c3c5ca]'">Recommended</p>
        <div v-if="tabItem == 'recommended'" class="h-[3px] mt-2 rounded-t-full bg-[#98B6FF]"></div>
      </div>
    </div>
    <div class="grid gap-4 grid-cols-12" v-if="tabItem == 'cast'">
        <div class=" col-span-6 " v-for="(cast, index) in casts" :key="index">
            <cast-card :cast="cast" />
        </div>
    </div>

    <div class="grid gap-4 grid-cols-12">
        <div class=" col-span-6" v-for="(movie, index) in similarMovies" :key="index">
            <movie-card :movie="movie"  />
        </div>
    </div>
  </div>
  <base-footer />
</template>
  
  <script setup>
import Casts from "../components/Casts.vue";
import CastCard from "../components/CastCard.vue";
import BaseFooter from "../components/BaseFooter.vue";
import BaseHeader from "../components/BaseHeader.vue";
import DetailsHero from "../components/DetailsHero.vue";
import MoreMovies from "../components/MoreMovies.vue";
import MovieCard from "../components/MovieCard.vue";
import axios from "axios";
import { ref, onMounted, watch } from "vue";
import { useRoute } from "vue-router";
import Overlay from "../components/Overlay.vue";

components: {
  BaseHeader, MoreMovies, BaseFooter, Casts, DetailsHero, Overlay,CastCard,MovieCard
}
const movie = ref([]);
const casts = ref([]);
const videos = ref([]);
const tabItem = ref('cast')
const movie_id = ref("");
const similarMovies = ref([]);
const loading = ref(true);
const route = useRoute();

const getMovies = async () => {
  await axios
    .get(
      `https://api.themoviedb.org/3/movie/${route.params.id}?api_key=5035e33b7502ccacbf835c91b3097af3`
    )
    .then((response) => {
      movie.value = response.data;
      loading.value = false;
    });
};

const getCasts = async () => {
  await axios
    .get(
      `https://api.themoviedb.org/3/movie/${route.params.id}/casts?api_key=5035e33b7502ccacbf835c91b3097af3`
    )
    .then((response) => {
      casts.value = response.data.cast;
    });
};
const getVideos = async () => {
  await axios
    .get(
      `https://api.themoviedb.org/3/movie/${route.params.id}/videos?api_key=5035e33b7502ccacbf835c91b3097af3`
    )
    .then((response) => {
      videos.value = response.data.results[0];
    });
};
const getSimilarMovies = async () => {
  await axios
    .get(
      `https://api.themoviedb.org/3/movie/${route.params.id}/similar?api_key=5035e33b7502ccacbf835c91b3097af3`
    )
    .then((response) => {
      similarMovies.value = response.data.results;
    });
};

// watchEffect(
//   movie_id,
//   (getMovies(), getCasts(), getVideos(), getSimilarMovies())
// );

watch(
  () => route.params.id,
  (newValue, oldValue) => {
    getMovies(),
      getCasts(),
      getVideos(),
      getSimilarMovies(),
      window.scrollTo(0, 0);
  },
  { immediate: true }
);

onMounted(() => {
  getMovies();
  getCasts();
  getVideos();
  getSimilarMovies();
});
</script>
  
  <style>
</style>