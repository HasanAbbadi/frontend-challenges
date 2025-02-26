<template>
  <div class="duel-screen">
    <div class="duel-screen__user">
      <span>You picked</span>
      <game-item
        :item="selectedItem"
        :showcase="true"
        :winner="result === 'win'"
      ></game-item>
    </div>

    <div class="duel-screen__computer">
      <span>The house picked</span>
      <div v-if="!computerItem" class="placeholder-item"></div>
      <game-item
        v-else
        class="play"
        :item="computerItem"
        :no-transition="result === 'draw'"
        :showcase="true"
        :winner="result === 'lose'"
      ></game-item>
    </div>

    <div class="duel-screen__result">
      <div v-if="result" class="duel-screen_result-content">
        <span>You {{ result }}</span>
        <button class="primary" @click="handlePlayAgain">Play again</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import GameItem from "src/components/game-item.vue";
import { ref, onMounted } from "vue";
const emit = defineEmits(["finished", "play-again"]);

const handlePlayAgain = async () => {
  if (!document.startViewTransition) {
    emit("play-again");
    return;
  }

  await document.startViewTransition(() => {
    emit("play-again");
  }).finished;
};

const props = defineProps({
  selectedItem: {
    type: String,
    required: true,
  },
});
const items = ["rock", "paper", "scissors"];

const computerItem = ref(null);
const result = ref(null);

onMounted(async () => {
  setTimeout(finishComputerChoice, 1000);
  setTimeout(() => {
    getResult();
    emit("finished", scoreLookup[result.value]);
  }, 2000);
});

const finishComputerChoice = () => {
  computerItem.value = items[Math.floor(Math.random() * items.length)];
};

const getResult = () => {
  result.value = lookupTable[props.selectedItem][computerItem.value];
};

const lookupTable = {
  rock: {
    rock: "draw",
    paper: "lose",
    scissors: "win",
  },
  paper: {
    rock: "win",
    paper: "draw",
    scissors: "lose",
  },
  scissors: {
    rock: "lose",
    paper: "win",
    scissors: "draw",
  },
};

const scoreLookup = {
  win: 1,
  lose: -1,
  draw: 0,
};
</script>

<style>
.duel-screen {
  display: grid;
  grid-template-columns: 1fr minmax(0, 0.6fr) 1fr;
  grid-template-rows: 1fr 1fr;
  grid-template-areas:
    "user result computer"
    "user result computer";
  width: 100%;

  @media (max-width: 768px) {
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 0.5fr 1fr;
    grid-template-areas:
      "user computer"
      "user computer"
      "result result";
  }
}

.duel-screen > div {
  display: grid;
  place-items: center;
  grid-row: span 2;
  grid-template-rows: subgrid;

  span {
    font-size: var(--fs-400);
    color: var(--clr-neutral-400);
    text-transform: uppercase;
    letter-spacing: 2px;

    @media (max-width: 768px) {
      font-size: var(--fs-300);
      order: 2;
    }
  }
}

.placeholder-item {
  width: 120px;
  background-color: rgba(from var(--clr-neutral-900) r g b / 0.125);
  border-radius: 50%;
  aspect-ratio: 1;
}

.duel-screen__user {
  grid-area: user;
}

.duel-screen__computer {
  grid-area: computer;
}

.duel-screen__result {
  grid-area: result;

  .duel-screen_result-content {
    display: grid;
    place-items: center;
    grid-row: span 2;
    opacity: 1;
    animation: fadeIn 0.5s ease-in-out;
    transform-origin: center;

    span {
      font-size: var(--fs-600);

      @media (max-width: 768px) {
        order: 1;
      }
    }

    button {
      width: 100%;
    }
  }
}

@keyframes fadeIn {
  from {
    transform: scaleX(0);
    opacity: 0;
  }
  to {
    transform: scaleX(1);
    opacity: 1;
  }
}
</style>
