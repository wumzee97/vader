<template>
    <div class=" lg:px-32 px-4 pt-20 bg-[#1B1F32]">
      <div class="flex justify-between">
        <p class="font-semibold text-[20px]">Cast</p>
  
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
      <div v-for="(cast,index) in casts" :key="index">
          <cast-card :cast="cast" class="mr-4"  :key="index" />

      </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import CastCard from "./CastCard.vue";
  import { ref } from "vue";
  components: {
    CastCard;
  }
  const props = defineProps(['casts'])
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