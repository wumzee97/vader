<template>
    <router-link :to="{name: 'Details', params: {id: movie.id}}">

        <div class="py-6 cursor-pointer">
          <div
            :style="`background-image: url(https://image.tmdb.org/t/p/original/${movie.poster_path})`"
            class="lg:w-[199px] lg:min-w-0 min-w-[48vw] h-[266px] rounded-[4px] bg-[#CEE8EF] bg-contain"
          ></div>
          <p class="font-semibold mt-3">{{movie.title}}</p>
          <p class="text-xs mt-2">
            <span class="pr-3 border-r border-[#7B808B]">{{new Date(movie.release_date).getFullYear()}}</span>
            <span class="pl-2">1h 53m</span>
          </p>
        </div>
    </router-link>
</template>

<script setup>
const props = defineProps(["movie"]);
</script>

<style>
</style>