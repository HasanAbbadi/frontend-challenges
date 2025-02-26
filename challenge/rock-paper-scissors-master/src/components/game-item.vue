<template>
  <div
    class="game-item"
    :class="`${item} ${showcase ? 'showcase' : ''} ${winner ? 'winner' : ''}`"
    :style="{
      viewTransitionName: noTransition ? null : `game-item-${item}`,
    }"
  >
    <div class="game-item__icon">
      <img :src="`src/assets/images/icon-${item}.svg`" :alt="item" />
    </div>
  </div>
</template>

<script setup>
defineProps({
  item: {
    type: String,
    required: true,
  },
  showcase: {
    type: Boolean,
    default: false,
  },
  winner: {
    type: Boolean,
    default: false,
  },
  noTransition: {
    type: Boolean,
    default: false,
  },
});
</script>

<style>
.game-item,
.game-item__icon {
  --shadow-offset: 6px;

  aspect-ratio: 1;
  border-radius: 50%;
  display: grid;
  place-items: center;
}

.game-item {
  width: 150px;
  position: relative;
  background: linear-gradient(to top, var(--bg));
  box-shadow: 0 var(--shadow-offset) 0 0 var(--shadow-color);
  cursor: pointer;
  transition: transform 0.125s ease-in-out;
  transform-style: preserve-3d;

  &.showcase {
    --scale: 1;
    cursor: default;
    transform: scale(var(--scale));

    @media (min-width: 768px) {
      --scale: 1.35;
    }

    &.play {
      animation: popUp 0.5s ease-in-out;
    }
  }

  &:not(.showcase):hover {
    transform: scale(1.05);
  }
}

@keyframes popUp {
  from {
    transform: scale(0);
  }

  to {
    transform: scale(var(--scale));
  }
}

.game-item__icon {
  width: 75%;
  background: linear-gradient(to top, var(--clr-white-gradient));
  box-shadow: inset 0 var(--shadow-offset) 0 0 rgba(50, 50, 50, 0.125);
  z-index: 3;
}

.game-item::after {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 50%;
  width: 100%;
  aspect-ratio: 1;
  z-index: 2;

  background: conic-gradient(
    transparent 40%,
    rgba(255, 255, 255, 0.25) 60%,
    transparent 100%
  );
  opacity: 0;
  transition: opacity 0.15s ease, transform 0.5s ease;
  transform-origin: center;
}

.game-item:not(.showcase):hover::after {
  transform: translate(-50%, -50%) rotate(270deg);
  opacity: 1;
}

.game-item.winner::before {
  animation: ripple 2s infinite ease;
}

.game-item.winner::before {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  translate: -50% -50%;
  width: 100%;
  aspect-ratio: 1/1;
  border-radius: 50%;
  background: radial-gradient(
    circle,
    #ffffff50 30%,
    #ffffff30 0%,
    #ffffff30 60%,
    #ffffff10 0%,
    #ffffff10 90%,
    #ffffff00 100%
  );
  transform: translateZ(-1px);
  scale: 1;
}

@keyframes ripple {
  0% {
    scale: 1;
    opacity: 0;
  }

  20% {
    opacity: 1;
  }

  100% {
    scale: 2;
    opacity: 0;
  }
}

.game-item {
  &.rock {
    --bg: var(--clr-rock-gradient);
    --shadow-color: var(--clr-rock-shadow);
  }

  &.paper {
    --bg: var(--clr-paper-gradient);
    --shadow-color: var(--clr-paper-shadow);
  }

  &.scissors {
    --bg: var(--clr-scissors-gradient);
    --shadow-color: var(--clr-scissors-shadow);
  }

  &.lizard {
    --bg: var(--clr-lizard-gradient);
    --shadow-color: var(--clr-lizard-shadow);
  }

  &.spock {
    --bg: var(--clr-spock-gradient);
    --shadow-color: var(--clr-spock-shadow);
  }
}
</style>
