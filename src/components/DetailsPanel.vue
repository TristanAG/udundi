<template>
    <transition name="slide-fade">
      <div v-if="isVisible" class="fixed inset-0 flex items-center justify-center z-50 p-4">
        <div class="bg-white text-gray-800 p-8 rounded-lg shadow-lg max-w-lg w-full relative">
          <button 
            @click="$emit('close')" 
            class="absolute top-4 right-4 text-gray-600 hover:text-gray-900 text-3xl font-bold leading-none"
          >
            &times;
          </button>
  
          <h2 class="text-3xl font-bold mb-4">More Details About Our Offer</h2>
          <p class="mb-4">
            Welcome to a deeper dive into what makes our offering unique. Here you'll find comprehensive information about our services, mission, and the value we bring. We are committed to excellence and transparency.
          </p>
          <p class="mb-4">
            Our team is dedicated to providing top-notch solutions tailored to your needs. Explore our features, benefits, and how we can help you achieve your goals.
          </p>
          <ul class="list-disc pl-5 mb-4">
            <li>Feature A: Detailed explanation of feature A.</li>
            <li>Feature B: Detailed explanation of feature B.</li>
            <li>Feature C: Detailed explanation of feature C.</li>
          </ul>
          <p>
            For any further questions, feel free to contact us.
          </p>
        </div>
      </div>
    </transition>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  
  const props = defineProps({
    isVisible: {
      type: Boolean,
      default: false
    }
  });
  
  const emits = defineEmits(['close']);
  </script>
  
  <style scoped>
  /* Transition styles for slide-fade */
  .slide-fade-enter-active,
  .slide-fade-leave-active {
    transition: all 0.3s ease-out;
  }
  
  .slide-fade-enter-from,
  .slide-fade-leave-to {
    transform: translateY(20px);
    opacity: 0;
  }
  </style>