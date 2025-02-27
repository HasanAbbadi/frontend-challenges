<template>
  <div class="clock">
    <div class="days">
      <flipper :number="days" />
      <span>Days</span>
    </div>
    <div class="hours">
      <flipper :number="hours" />
      <span>Hours</span>
    </div>
    <div class="minutes">
      <flipper :number="minutes" />
      <span>Minutes</span>
    </div>
    <div class="seconds">
      <flipper :number="seconds" />
      <span>Seconds</span>
    </div>
  </div>
</template>

<style>
.clock {
  gap: 1rem;
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 1rem;
}

.days,
.hours,
.minutes,
.seconds {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;

  span {
    color: var(--clr-secondary);
    font-size: 12px;

    @media (max-width: 768px) {
      letter-spacing: 5rem;
      display: -webkit-box;
      -webkit-line-clamp: 1;
      -webkit-box-orient: vertical;
      overflow: hidden;
      max-width: 1.5ch;
    }
  }
}
</style>

<script setup>
import { ref } from "vue";
import flipper from "src/components/flipper.vue";
const days = ref(0);
const hours = ref(0);
const minutes = ref(0);
const seconds = ref(0);

const props = defineProps({
  launchDateTime: {
    type: String,
    required: true,
  },
});

const updateCountdown = () => {
  const now = new Date();
  const launchTime = new Date(props.launchDateTime);

  if (isNaN(now.getTime()) || isNaN(launchTime.getTime())) {
    days.value = 0;
    hours.value = 0;
    minutes.value = 0;
    seconds.value = 0;
    return;
  }

  const timeLeft = launchTime.getTime() - now.getTime();

  if (timeLeft <= 0) {
    days.value = 0;
    hours.value = 0;
    minutes.value = 0;
    seconds.value = 0;
    return;
  }

  days.value = Math.floor(timeLeft / (1000 * 60 * 60 * 24));
  hours.value = Math.floor(
    (timeLeft % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
  );
  minutes.value = Math.floor((timeLeft % (1000 * 60 * 60)) / (1000 * 60));
  seconds.value = Math.floor((timeLeft % (1000 * 60)) / 1000);
};

setInterval(updateCountdown, 1000);
</script>

<style></style>
