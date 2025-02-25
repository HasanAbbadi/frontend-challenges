<template>
  <div class="balance-card">
    <div class="balance-card__details">
      <span class="balance-card__details-label">My balance</span>
      <span class="balance-card__details-amount">${{ balance }}</span>
    </div>
    <div class="balance-card__logo">
      <img src="src/assets/images/logo.svg" alt="Logo" />
    </div>
  </div>
</template>

<script setup>
defineProps({
  balance: {
    type: Number,
    required: true,
  },
});
</script>

<style>
.balance-card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: var(--clr-primary);
  color: var(--clr-neutral-100);
  padding: 1.5rem;
  border-radius: var(--br-300);
  width: 100%;
}

.balance-card__details {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.balance-card__details-label {
  font-size: var(--fs-200);
}

.balance-card__details-amount {
  font-size: var(--fs-400);
  font-weight: var(--fw-bold);
}
</style>
