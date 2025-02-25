<template>
  <div class="chart-bar">
    <div
      class="chart-bar__tooltip"
      :class="{ 'chart-bar__tooltip--visible': isHovered }"
      :style="{ bottom: `${barHeight + 30}px` }"
    >
      ${{ value.toFixed(2) }}
    </div>
    <svg
      class="chart-bar__bar"
      width="40"
      height="150"
      @mouseenter="isHovered = true"
      @mouseleave="isHovered = false"
    >
      <rect
        x="0"
        :y="150 - barHeight"
        width="40"
        :height="barHeight"
        rx="5"
        :class="{ 'chart-bar__bar--active': isToday(label) }"
      />
    </svg>
    <div class="chart-bar__label">{{ label }}</div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const props = defineProps({
  value: {
    type: Number,
    required: true,
  },
  label: {
    type: String,
    required: true,
  },
});

const isHovered = ref(false);

// Scale the bar height to fit within the SVG
const barHeight = computed(() => {
  return (props.value / 100) * 250; // Adjust the denominator based on your max value
});

const isToday = (weekDay) => {
  const today = new Date();
  const dayNum = today.getDay();
  const days = ["sun", "mon", "tue", "wed", "thu", "fri", "sat"];
  const todayStr = days[dayNum];
  return todayStr === weekDay.toLowerCase();
};
</script>

<style>
.chart-bar {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-end;
  position: relative;
}

.chart-bar__tooltip {
  position: absolute;
  bottom: 40px; /* Default position */
  left: 50%;
  transform: translateX(-50%);
  background-color: var(--clr-neutral-900);
  color: var(--clr-neutral-100);
  font-weight: var(--fw-bold);
  padding: 5px 8px;
  border-radius: 5px;
  font-size: 12px;
  opacity: 0;
  transition: opacity 0.2s ease;
  pointer-events: none;
  z-index: 1;
}

.chart-bar__tooltip--visible {
  opacity: 1;
}

.chart-bar__bar {
  fill: var(--clr-primary);
  transition: fill 0.2s ease;
  cursor: pointer;
}

.chart-bar__bar:hover {
  opacity: 0.8;
}

.chart-bar__bar--active {
  fill: var(--clr-secondary);
}

.chart-bar__label {
  margin-top: 8px;
  font-size: 12px;
  color: var(--clr-neutral-800);
}
</style>
