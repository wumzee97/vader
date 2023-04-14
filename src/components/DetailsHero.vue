<template>
  <div>
    <div class="flex justify-center items-center">
      <div
        :style="`background-image: url(https://image.tmdb.org/t/p/original/${movie.backdrop_path})`"
        class="lg:h-[750px] h-[500px] w-screen flex items-center bg-[url('../assets/Hero.png')] bg-no-repeat bg-cover"
      >
        <div
          class="w-screen grid gap-0 items-center lg:px-32 px-4 grid-cols-12 h-full backdrop-brightness-50"
        >
          <div class="lg:col-span-6 col-span-12 text-left">
            <p class="text-sm">
              <span class="text-[#E8BA35]">Featured</span> |
              {{ new Date(movie.release_date).getFullYear() }} |
              <span v-for="(gen, index) in movie.genres" :key="index"
                >{{ gen.name }}{{ index != movie.genres.length ? ", " : null }}
              </span>
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
              <button
                @click="isOpen = true"
                class="h-[44px] w-[146px] font-medium flex items-center justify-center bg-[#3772FF] rounded-md"
              >
                <img src="../assets/play-circle.svg" alt="" />
                <span class="ml-2">Watch now</span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

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
  </div>
</template>

<script setup>
import Modal from "./Modal.vue";
import { ref } from "vue";

const props = defineProps(["movie", 'video']);
components: {
  Modal;
}
const isOpen = ref(false);
</script>

<style>
</style>