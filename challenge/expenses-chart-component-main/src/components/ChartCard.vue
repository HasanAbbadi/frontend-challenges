<template>
  <div class="chart-card">
    <h3 class="header">{{ title }}</h3>
    <slot></slot>
    <div class="footer">
      <span class="total">Total this month</span>
      <div class="footer__details">
        <span class="total-amount">${{ totalAmount }}</span>
        <div class="footer__details-percentage">
          <span class="percentage">2.4%</span>
          <span class="percentage-label">from last month</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: {
    type: String,
    default: "Chart",
  },
  totalAmount: {
    type: Number,
    default: 0,
  },
});
</script>

<style>
.chart-card {
  background-color: var(--clr-neutral-100);
  padding: 2rem;
  border-radius: var(--br-300);
  color: var(--clr-neutral-900);
  width: 100%;
}

.header {
  font-size: var(--fs-400);
  font-weight: var(--fw-bold);
  color: var(--clr-neutral-900);
}

.footer {
  border-top: 1px solid var(--clr-neutral-200);
  padding-top: 1rem;
}

.footer__details {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer__details-percentage {
  display: flex;
  align-items: flex-end;
  flex-direction: column;
}

.percentage-label,
.total {
  font-size: var(--fs-200);
  color: var(--clr-neutral-800);
}

.total-amount,
.percentage {
  color: var(--clr-neutral-900);
}

.total-amount {
  font-size: var(--fs-600);
  font-weight: var(--fw-bold);
}

.percentage {
  font-weight: var(--fw-bold);
}
</style>
