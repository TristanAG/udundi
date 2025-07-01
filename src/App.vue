<template>
  <div class="h-screen w-screen flex flex-col md:flex-row overflow-hidden md:h-screen relative">
    <div class="w-full md:w-1/3 bg-[#6A1B1A] text-white flex flex-col justify-center pl-10 pt-70 h-1/4 md:h-full">
      <h1
  class="text-5xl md:text-9xl font-serif leading-tight relative z-10 pl-10 md:pl-20 lg:pl-24 -mt-50 md:mt-0"
>
  Explore
</h1>



      <!-- Button with responsive padding -->
      <button
        ref="openBtn"
        @click="openPanel"
        :class="[
          'flex items-center text-white py-2 gap-3 relative z-10',
          'transition-all duration-[300ms] ease-[cubic-bezier(0.22,1,0.36,1)]',
          'px-5 md:px-20 lg:px-[15%]',  // responsive horizontal padding
          { 'opacity-0 pointer-events-none': !showButton }
        ]"
      >
        <span class="text-2xl flex-shrink-0">
          <img src="./assets/Plus.svg" alt="Plus" class="w-6 h-6" />
        </span>
        <span class="text-sm tracking-wide whitespace-nowrap flex-shrink-0">More Details</span>
      </button>

    </div>

    <div class="w-full md:w-2/3 relative h-3/4 md:h-full">
      <img
        src="./assets/Coding-Challenge-Image.png"
        alt="Forest"
        class="object-cover w-full h-full"
      />

      <div class="absolute bottom-6 right-6 flex flex-col space-y-4">
        <a
          href="#"
          class="w-10 h-10 rounded-full flex items-center justify-center hover:bg-gray-200 transition"
        >
          <img
            src="./assets/Facebook.svg"
            alt="Facebook"
          />
        </a>
        <a
          href="#"
          class="w-10 h-10 rounded-full flex items-center justify-center hover:bg-gray-200 transition"
        >
          <img
            src="./assets/Instagram.svg"
            alt="Instagram"
          />
        </a>
      </div>
    </div>

    <DetailsPanel
      v-if="isPanelOpen"
      :startRect="buttonRect"
      @close="closePanel"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
import DetailsPanel from "./components/DetailsPanel.vue";

const isPanelOpen = ref(false);
const buttonRect = ref(null);
const openBtn = ref(null);
const showButton = ref(true);

const openPanel = () => {
  if (openBtn.value) {
    buttonRect.value = openBtn.value.getBoundingClientRect();
  }
  isPanelOpen.value = true;
  showButton.value = false;
};

const closePanel = () => {
  isPanelOpen.value = false;
  showButton.value = true;
};
</script>

<style scoped>
button {
  transition: all 0.3s cubic-bezier(0.22, 1, 0.36, 1);
}
</style>
