<template>
    <div
        class="fixed z-50 bg-white shadow-lg overflow-hidden"
        :style="panelStyle"
        :class="flareClass"
    >
        <button
            @click="close"
            class="absolute top-4 right-4 text-gray-600 hover:text-gray-900 text-3xl font-bold leading-none z-10"
            aria-label="Close details panel"
        >
            &times;
        </button>
  
        <div class="panel-content max-w-lg mx-auto mt-12">
            <h2 class="text-3xl font-bold mb-4 text-[#6A1B1A]">Explore</h2>
  
            <p class="mb-4">
                Sed ut perspiciatis unde omnis iste natus error sit voluptatem 
                accusantium doloremque laudantium, totam rem aperiam, eaque ipsa 
                quae ab illo inventore veritatis et quasi architecto beatae vitae 
                dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit 
                aspernatur aut odit aut fugit, sed quia consequuntur magni dolores 
                eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, 
                 dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, 
                 sed quia non numquam eius modi tempora incidunt ut labore et dolore 
                 magnam aliquam quaerat voluptatem. Ut enim ad minima veniam, quis 
                 nostrum exercitationem ullam corporis suscipit laboriosam, nisi ut 
                 aliquid ex ea commodi consequatur? 
            </p>

            <button
  class="text-white px-6 py-3 rounded font-semibold"
  style="background: linear-gradient(to right, #611818, #A36754);"
>
  Read More
</button>
        </div>
    </div>
</template>
  
<script setup>
    import { ref, watch, nextTick } from "vue";
  
    const props = defineProps({
        startRect: Object,
    });
  
    const emits = defineEmits(["close"]);
  
    const panelStyle = ref({});
    const flareClass = ref("");
  
    const expandedStyle = {
        top: "50%",
        left: "50%",
        width: "600px",
        height: "500px",
        // transform: "translate(-33%, -50%)",
        
        overflow: "auto",
        position: "fixed",
        backgroundColor: "white",
        zIndex: 9999,
        transition: "all 0.5s cubic-bezier(0.8, 1, 0.36, 1)",
    };
  
    const setStartStyle = (rect) => ({
        position: "fixed",
        top: `${rect.top + 27}px`,
        left: `${rect.left + 230}px`,
        width: `${rect.width}px`,
        height: `${rect.height}px`,
        borderRadius: "12px",
        overflow: "hidden",
        backgroundColor: "white",
        zIndex: 9999,
        width: "60px",
        height: "60px",
        borderRadius: "50%",
        transform: "translate(0, 0)",
        transition: "all 0.5s cubic-bezier(0.22, 1, 0.36, 1)"
    });
  
    const animateToFull = () => {
        nextTick(() => {
            flareClass.value = "flare-grow";
            panelStyle.value = expandedStyle;
        });
    };
  
    const animateClose = () => {
        flareClass.value = "flare-shrink";

        // Start moving the panel back to its origin rectangle
        panelStyle.value = setStartStyle(props.startRect);

        setTimeout(() => {
            emits("close");
        }, 500);
    };
  
    watch (
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

    .flare-grow {
        animation: flareGrow 0.5s ease forwards;
    }

    .flare-shrink {
        animation: flareShrink 0.5s ease forwards;
    }

    @keyframes flareGrow {
        0% {
            transform: translate(-60%, -50%) scale(1);
            border-radius: 10%;
        }
        40% {
            transform: translate(-60%, -50%) scale(1, 1.04);
            border-radius: 7%;
        }
        70% {
            transform: translate(-60%, -50%) scale(1.18, 1.02);
            border-radius: 4%;
        }
        100% {
            transform: translate(-60%, -50%) scale(1);
            border-radius: 0px;
        }
    }

    @keyframes flareShrink {
        0% {
            transform: translate(-60%, -50%) scale(1);
            border-radius: 16px;
        }
        40% {
            transform: translate(-60%, -50%) scale(1.18, 1.02);
            border-radius: 20px;
        }
        70% {
            transform: translate(-60%, -50%) scale(1, 1.04);
            border-radius: 20px;
        }
        100% {
            transform: translate(-60%, -50%) scale(0);
            border-radius: 12px;
        }
    }

    @media (max-width: 768px) {
        div[style] {
            width: 90vw !important;
            height: 80vh !important;
            top: 10vh !important;
            left: 5vw !important;
            transform: none !important;
            border-radius: 16px !important;
            padding: 8px;
        }
    }
</style>
  