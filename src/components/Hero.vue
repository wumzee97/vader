<template>
  
  <carousel :autoplay="6000" class="py-0 h-auto">
    <slide class="w-screen h-full" v-for="(movie, index) in movies" :key="index">
      <div class="flex justify-center items-center h-full">
        <div
          :style="`background-image: url(https://image.tmdb.org/t/p/original/${movie.backdrop_path})`"
          class="lg:h-[750px] h-[500px]  w-screen flex items-center bg-[url('../assets/Hero.png')] bg-no-repeat bg-cover"
        >
          <div
            class="w-screen grid gap-0 items-center lg:px-32 px-4 grid-cols-12 h-full backdrop-brightness-50"
          >
            <div class="lg:col-span-6 col-span-12 text-left">
              <p class="text-sm">
                <span class="text-[#E8BA35]">Featured</span> |
                {{ new Date(movie.release_date).getFullYear() }} | Action,
                Sci-Fi, Drama
              </p>
              <h2 class="font-semibold mt-4 text-[#FDFDFD] text-[42px]">
                {{ movie.title }}
              </h2>
              <div class="flex mt-2">
                <p class="flex items-center">
                  <img src="../assets/star.svg" alt="" />
                  {{ movie.vote_average }}
                </p>

                <div class="ml-8 border p-1 px-3 rounded-full">
                  <span class="text-sm">16+</span>
                </div>
              </div>
              <p class="my-6">
                {{ movie.overview }}
              </p>
              <div class="flex">
                <button @click="getVideos(movie.id)"
                  class="h-[44px] w-[146px] font-medium flex items-center justify-center bg-[#3772FF] rounded-md"
                >
                  <img src="../assets/play-circle.svg" alt="" />
                  <span class="ml-2">Watch now</span>
                </button>
                <router-link
                  :to="{ name: 'Details', params: { id: movie.id } }"
                  v-if="showlearnmore"
                >
                  <button
                    class="h-[44px] ml-3 w-[146px] font-medium border border-[#98B6FF] flex items-center justify-center bg-[#21354A] rounded-md"
                  >
                    <img src="../assets/vuesax/bold/info-circle.svg" alt="" />
                    <span class="ml-2">Learn more</span>
                  </button>
                </router-link>
              </div>
            </div>
          </div>
        </div>
      </div>
    </slide>

    <!-- <template #addons>
      <navigation />
      <pagination />
    </template> -->
  </carousel>
  <modal v-if="isOpen" :isOpen="isOpen" @close="isOpen = false">
      <iframe
        width="100%"
        height="315"
        :src="`https://www.youtube.com/embed/${video}?autoplay=1`"
        title="YouTube video player"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen
      ></iframe>
    </modal>
</template>

<script setup>
import { ref, onMounted, computed } from "vue";
import axios from 'axios'

import Overlay from "../components/Overlay.vue";
import "vue3-carousel/dist/carousel.css";
import Modal from "./Modal.vue";
import { Carousel, Slide, Pagination, Navigation } from "vue3-carousel";
components: {
 Modal, Overlay, Carousel, Slide, Pagination, Navigation;
}
const isOpen = ref(false)
const video = ref(null)

const props = defineProps(["showlearnmore", 'movies']);

const getVideos = async (id) => {
  await axios
    .get(
      `https://api.themoviedb.org/3/movie/${id}/videos?api_key=5035e33b7502ccacbf835c91b3097af3`
    )
    .then((response) => {
      video.value = response.data.results[0].key
      isOpen.value = true
    });
};
</script>

<style>
.bgg {
  background-image: url("../assets/starwar.jpeg");
}
</style>