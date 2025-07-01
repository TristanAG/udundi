<template>
  <div class="h-screen w-screen flex flex-col md:flex-row overflow-hidden md:h-screen relative">
    <div
      class="w-full md:w-1/3 bg-[#6A1B1A] text-white flex flex-col justify-center p-10 h-1/4 md:h-full"
    >
      <h1 class="text-5xl md:text-7xl font-serif leading-tight mb-8">Explore</h1>
      <button
        ref="openBtn"
        @click="openPanel"
        class="flex items-center text-white px-5 py-2 gap-3 hover:bg-white hover:text-[#6A1B1A] transition"
      >
        <span class="text-2xl">+</span>
        <span class="text-sm tracking-wide">More Details</span>
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
          class="w-10 h-10 bg-white rounded-full flex items-center justify-center hover:bg-gray-200 transition"
        >
          <img
            src="https://img.icons8.com/ios-filled/24/000000/facebook.png"
            alt="Facebook"
          />
        </a>
        <a
          href="#"
          class="w-10 h-10 bg-white rounded-full flex items-center justify-center hover:bg-gray-200 transition"
        >
          <img
            src="https://img.icons8.com/ios-filled/24/000000/instagram-new.png"
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

const openPanel = () => {
  if (openBtn.value) {
    buttonRect.value = openBtn.value.getBoundingClientRect();
  }
  isPanelOpen.value = true;
};

const closePanel = () => {
  isPanelOpen.value = false;
};
</script>
