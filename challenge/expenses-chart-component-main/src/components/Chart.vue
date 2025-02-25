<template>
  <div class="chart">
    <chart-bar
      v-for="dataPoint in dataPoints"
      :key="dataPoint.label"
      :value="dataPoint.amount"
      :label="dataPoint.day"
    ></chart-bar>
  </div>
</template>

<script setup>
import ChartBar from "./ChartBar.vue";

defineProps({
  dataPoints: {
    type: Array,
    required: true,
  },
});
</script>

<style>
.chart {
  display: flex;
  justify-content: space-between;
  gap: var(--fs-100);
  padding-block: 1rem;
}
</style>
