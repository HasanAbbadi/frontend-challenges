<template>
  <div class="rock-paper-scissors">
    <game-item
      v-for="item in items"
      :key="item"
      :item="item"
      @click="selectItem(item)"
    ></game-item>
  </div>
</template>

<script setup>
import GameItem from "src/components/game-item.vue";

const items = ["rock", "paper", "scissors"];

const emit = defineEmits(["selected"]);

const selectItem = async (item) => {
  if (!document.startViewTransition) {
    emit("selected", item);
    return;
  }

  await document.startViewTransition(() => {
    emit("selected", item);
  }).finished;
};
</script>

<style>
.rock-paper-scissors {
  display: grid;
  place-items: center;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(2, 1fr);

  background-image: url("src/assets/images/bg-triangle.svg");
  background-position: center;
  background-repeat: no-repeat;
  background-position-y: 60px;

  width: 100%;
  @media (min-width: 768px) {
    width: 80%;
  }
}

.rock-paper-scissors > * {
  &:nth-child(1) {
    grid-column: 1 / 3;
    grid-row: 1;
  }

  &:nth-child(2) {
    grid-column: 3 / 5;
    grid-row: 1;
  }

  &:nth-child(3) {
    grid-column: 2 / 4;
    grid-row: 2;
  }
}
</style>
