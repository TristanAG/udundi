<template>
    <div
      class="fixed z-50 bg-white shadow-lg rounded-lg overflow-hidden"
      :style="panelStyle"
    >
      <button
        @click="close"
        class="absolute top-4 right-4 text-gray-600 hover:text-gray-900 text-3xl font-bold leading-none z-10"
        aria-label="Close details panel"
      >
        &times;
      </button>
  
      <div class="panel-content p-8 max-w-lg mx-auto mt-12">
        <h2 class="text-3xl font-bold mb-4">More Details About Our Offer</h2>
  
        <p class="mb-4">
          Welcome to a deeper dive into what makes our offering unique. Here you'll
          find comprehensive information about our services, mission, and the value
          we bring. We are committed to excellence and transparency.
        </p>
  
        <p class="mb-4">
          Our team is dedicated to providing top-notch solutions tailored to your
          needs. Explore our features, benefits, and how we can help you achieve
          your goals.
        </p>
  
        <ul class="list-disc pl-5 mb-4">
          <li>Feature A: Detailed explanation of feature A.</li>
          <li>Feature B: Detailed explanation of feature B.</li>
          <li>Feature C: Detailed explanation of feature C.</li>
        </ul>
  
        <p>For any further questions, feel free to contact us.</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, watch, nextTick } from "vue";
  
  const props = defineProps({
    startRect: {
      type: Object,
      required: false,
      default: null,
    },
  });
  
  const emits = defineEmits(["close"]);
  
  const panelStyle = ref({});
  
  const expandedStyle = {
    top: "50%",
    left: "50%",
    width: "600px",
    height: "400px",
    transform: "translate(-50%, -50%)",
    borderRadius: "44px",
    overflow: "auto",
    position: "fixed",
    backgroundColor: "white",
    zIndex: 9999,
    transition: "all 0.5s cubic-bezier(0.22, 1, 0.36, 1)",
    animation: "flareGrow 0.5s ease forwards",
  };
  
  const setStartStyle = (rect) => ({
    position: "fixed",
    top: `${rect.top}px`,
    left: `${rect.left}px`,
    width: `${rect.width}px`,
    height: `${rect.height}px`,
    borderRadius: "12px",
    overflow: "hidden",
    backgroundColor: "white",
    zIndex: 9999,
    transform: "translate(0, 0)",
  });
  
  const animateToFull = () => {
    nextTick(() => {
      panelStyle.value = expandedStyle;
    });
  };
  
  const animateClose = () => {
    if (!props.startRect) return emits("close");
  
    panelStyle.value = setStartStyle(props.startRect);
  
    setTimeout(() => {
      emits("close");
    }, 500);
  };
  
  watch(
    () => props.startRect,
    (newVal) => {
      if (newVal) {
        panelStyle.value = setStartStyle(newVal);
  
        requestAnimationFrame(() => {
          animateToFull();
        });
      }
    },
    { immediate: true }
  );
  
  const close = () => {
    animateClose();
  };
  </script>
  
  <style scoped>
  button {
    cursor: pointer;
  }
  
  /* Top bulge animation: scales top edge horizontally */
  @keyframes flareGrow {
  0% {
    transform: translate(var(--start-left), var(--start-top)) scale(1);
    border-radius: 12px;
    box-shadow:
      inset 0 0 0 0 rgba(255, 255, 255, 0),
      inset 0 0 0 0 rgba(255, 255, 255, 0),
      inset 0 0 0 0 rgba(255, 255, 255, 0),
      inset 0 0 0 0 rgba(255, 255, 255, 0);
  }
  40% {
    transform: translate(-50%, -50%) scale(3.2, 3.1);
    border-radius: 30px 30px 30px 30px;
    box-shadow:
      inset 15px 0 10px -10px rgba(255, 255, 255, 0.3),
      inset -15px 0 10px -10px rgba(255, 255, 255, 0.3),
      inset 0 15px 10px -10px rgba(255, 255, 255, 0.3),
      inset 0 -15px 10px -10px rgba(255, 255, 255, 0.3);
  }
  70% {
    transform: translate(-50%, -50%) scale(2.8, 2.9);
    border-radius: 18px 18px 18px 18px;
    box-shadow:
      inset 8px 0 8px -8px rgba(255, 255, 255, 0.2),
      inset -8px 0 8px -8px rgba(255, 255, 255, 0.2),
      inset 0 8px 8px -8px rgba(255, 255, 255, 0.2),
      inset 0 -8px 8px -8px rgba(255, 255, 255, 0.2);
  }
  100% {
    transform: translate(-50%, -50%) scale(3);
    border-radius: 16px 16px 16px 16px;
    box-shadow:
      inset 0 0 0 0 rgba(255, 255, 255, 0),
      inset 0 0 0 0 rgba(255, 255, 255, 0),
      inset 0 0 0 0 rgba(255, 255, 255, 0),
      inset 0 0 0 0 rgba(255, 255, 255, 0);
  }
}

  </style>
  