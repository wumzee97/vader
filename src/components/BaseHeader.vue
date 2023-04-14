<template>
  <div>
    <header
      class="lg:px-32 relative px-4 flex items-center justify-between h-20 bg-[#1D283C]"
    >
      <div>
        <router-link :to="{ name: 'Home' }">
          <img src="../assets/Logo.svg" alt="" />
        </router-link>
      </div>
      <div class="hidden lg:block">
        <base-search-input />
      </div>
      <div class="lg:hidden">
        <img
          v-if="showSearch"
          @click="showSearch = false"
          src="../assets/Modals/menu.svg"
          alt=""
        />
        <img
          v-else
          @click="showSearch = true"
          src="../assets/InputText/search-normal.svg"
          class="h-[24px] w-[24px]"
          alt=""
        />
      </div>
    </header>
    <transition name="switch">

        <div class="h-screen  z-50 fixed w-screen backdrop-blur-sm backdrop-brightness-50" v-if="showSearch">
    
            <div  class="bg-[#1B1F32] p-6  w-full">
                <base-search-input />
              </div>
        </div>  
    </transition>
   
  </div>
</template>

<script setup>
import BaseSearchInput from "./BaseSearchInput.vue";
import { ref } from "vue";
components: {
  BaseSearchInput;
}
const showSearch = ref(false);
</script>

<style scoped>
  .switch-enter-from,
  .switch-leave-to {
    opacity: 0;
    transform: translateY(20px);
  }
  .switch-enter-active{
    transition: all 0.5s ease;
  }
  .switch-leave-active {
    transition: all 0.5s ease;
    position: absolute;
    width: 100%;
  }
</style>