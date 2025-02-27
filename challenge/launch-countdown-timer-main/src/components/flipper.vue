<template>
  <div class="flipper">
    <div class="top">
      <div class="text">{{ String(displayNumber).padStart(2, "0") }}</div>
    </div>
    <div class="bottom">
      <div class="text">{{ String(displayNumber).padStart(2, "0") }}</div>
    </div>

    <div v-if="isFlipping" class="top new">
      <div class="text">{{ String(oldNumber).padStart(2, "0") }}</div>
    </div>
    <div v-if="isFlipping" class="bottom new">
      <div class="text">{{ String(displayNumber).padStart(2, "0") }}</div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  number: {
    type: Number,
    required: true,
  },
});

const oldNumber = ref(props.number);
const displayNumber = ref(props.number);
const isFlipping = ref(false);

watch(
  () => props.number,
  (newVal, oldVal) => {
    if (newVal === oldVal) return;
    oldNumber.value = oldVal;
    isFlipping.value = true;

    // Update the display number after half the animation time
    setTimeout(() => {
      displayNumber.value = newVal;
    }, 300);

    // Reset the flipping state after animation completes
    setTimeout(() => {
      isFlipping.value = false;
    }, 600);
  }
);
</script>

<style>
.flipper {
  position: relative;
  width: 100%;
  height: 100px;
  border-radius: var(--br-100);
  perspective: 1000px;
  overflow: hidden;
  box-shadow: 0 6px 0px 0 rgba(0, 0, 0, 0.25);

  &::before,
  &::after {
    content: "";
    position: absolute;
    width: 6px;
    height: 6px;
    background: var(--clr-bg);
    border-radius: 50%;
    top: 50%;
    transform: translateY(-50%);
    z-index: 3;
  }

  &::before {
    left: -3px;
  }

  &::after {
    right: -3px;
  }
}

.top,
.bottom {
  position: absolute;
  width: 100%;
  height: 50%;
  overflow: hidden;
  backface-visibility: hidden;
  .text {
    position: absolute;
    width: 100%;
    height: 200%;
    opacity: 0.8;
    color: var(--clr-primary);
    font-size: var(--fs-900);
    font-family: "Arial", sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    letter-spacing: normal;

    @media (max-width: 768px) {
      font-size: var(--fs-700);
    }
  }
}

.top {
  background-color: hsl(from var(--clr-neutral-500) h s calc(l - 5));
  transform-origin: bottom;

  .text {
    bottom: -100%;
  }
}

.bottom {
  bottom: 0;
  background-color: var(--clr-neutral-500);

  .text {
    top: -100%;
  }
}

.top.new {
  z-index: 2;
  transform-origin: bottom center;
  animation: rotate-top 0.6s ease-in-out forwards;
  transform-style: preserve-3d;

  &::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0);
    animation: shadow 0.6s ease-in-out forwards;
  }
}

.bottom.new {
  z-index: 1;
  transform-origin: top center;
  animation: rotate-bottom 0.4s ease-in-out forwards;
  transform-style: preserve-3d;
}

@keyframes shadow {
  0% {
    background: rgba(0, 0, 0, 0);
  }
  50% {
    background: rgba(0, 0, 0, 0.2);
  }
  100% {
    background: rgba(0, 0, 0, 0);
  }
}

@keyframes rotate-top {
  0% {
    transform: rotateX(0);
  }
  100% {
    transform: rotateX(-180deg);
  }
}

@keyframes rotate-bottom {
  0% {
    transform: rotateX(180deg);
    opacity: 0;
  }
  49.99% {
    transform: rotateX(180deg);
    opacity: 0;
  }
  50% {
    opacity: 0.8;
  }
  100% {
    transform: rotateX(0deg);
    opacity: 1;
  }
}
</style>
