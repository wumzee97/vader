<template>
  <div class="min-h-[498px] lg:px-32 px-4 py-16 bg-[#1B1F32]">
    <div class="flex justify-between">
      <p class="font-semibold text-[20px]">{{ title || 'Movies for you' }}</p>

      <div class="flex">
        <img
          @click="scrollMovieLeft"
          class="cursor-pointer"
          src="../assets/arrow-left.svg"
          alt=""
        />
        <img
          src="../assets/arrow-right.svg"
          @click="scrollMovieRight"
          class="ml-5 cursor-pointer"
          alt=""
        />
      </div>
    </div>
    <div
      class="flex overflow-x-scroll scroll-smooth scrollbar-hide"
      ref="moviebox"
    >
    <div v-for="(movie,index) in movies" :key="index" class="mr-4">
        <movie-card :movie="movie"   />
    </div>
    </div>
  </div>
</template>

<script setup>
import MovieCard from "./MovieCard.vue";
import { ref } from "vue";
import axios from 'axios'
const props = defineProps(['title', 'movies'])
components: {
  MovieCard;
}
const moviebox = ref(null);
const scrollMovieRight = () => {
  var element = moviebox.value;
  element.scrollLeft += 300;
};
const scrollMovieLeft = () => {
  var element = moviebox.value;
  element.scrollLeft -= 300;
};


</script>

<style scoped>
.scrollbar-hide::-webkit-scrollbar {
  display: none;
}

/* For IE, Edge and Firefox */
.scrollbar-hide {
  -ms-overflow-style: none; /* IE and Edge */
  scrollbar-width: none; /* Firefox */
}
</style>