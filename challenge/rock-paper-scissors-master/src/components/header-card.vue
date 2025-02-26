<template>
  <div class="header-card">
    <div class="header-card__logo">
      <img src="src/assets/images/logo.svg" alt="logo" />
    </div>
    <div class="header-card__score">
      <h5>Score</h5>
      <p>{{ score }}</p>
    </div>
  </div>
</template>

<script setup>
defineProps({
  score: {
    type: Number,
    required: true,
  },
});
</script>

<style>
.header-card {
  width: min(90%, 600px);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.75rem 1.25rem;
  border: 3px solid var(--clr-header-outline);
  border-radius: var(--br-300);
}

.header-card__logo {
  height: 90px;

  img {
    height: 100%;
  }
}

.header-card__score {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  padding: 0.75rem 2.25rem;
  background-color: var(--clr-neutral-000);
  border-radius: var(--br-200);
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.1);
  color: var(--clr-dark-text);

  h5 {
    color: var(--clr-score-text);
    font-size: var(--fs-100);
    letter-spacing: 0.125em;
    text-transform: uppercase;
    line-height: 1;
  }

  p {
    color: var(--clr-dark-text);
    font-size: var(--fs-800);
    font-weight: var(--fw-bold);
    line-height: 1;
  }
}
</style>
