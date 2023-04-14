<template>
    <div class="py-6">
      <div class="lg:w-[199px] w-full h-[199px] rounded-[4px] bg-[#CEE8EF] bg-cover" :style="`background-image: url(https://image.tmdb.org/t/p/original/${cast.profile_path})`">
  
      </div>
      <p class="font-semibold mt-3">{{cast.name}}</p>
      <p class="text-xs mt-2"><span class="pr-3  ">{{cast.character}}</span></p>
    </div>
  </template>
  
  <script setup>
    const props = defineProps(['cast'])
  
  </script>
  
  <style>
  
  </style>