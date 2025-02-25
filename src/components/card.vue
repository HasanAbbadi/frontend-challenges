<template>
  <div class="card">
    <div class="header">
      <h5>
        <a :href="`./challenge/${path}`">{{ title }}</a>
      </h5>
      <h6>
        <a class="source-link" :href="source" target="_blank">{{
          sourceName
        }}</a>
      </h6>
    </div>
    <div class="body">
      <div class="tags">
        <span v-for="tag in tags" :key="tag" class="tag" :class="tag">{{
          tag
        }}</span>
      </div>
      <h6 class="date">{{ formattedDate }}</h6>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  path: {
    type: String,
    required: true,
  },
  tags: {
    type: Array,
    required: true,
  },
  source: {
    type: String,
    required: true,
  },
  date: {
    type: String,
    required: false,
  },
});

const sourceName = computed(() => {
  const url = new URL(props.source);
  return url.hostname.replace("www.", "").split(".")[0];
});

const formattedDate = computed(() => {
  const date = new Date(props.date);
  return date.toLocaleDateString("en-US", {
    month: "short",
    day: "numeric",
    year: "numeric",
  });
});
</script>

<style>
.card {
  padding: 1rem;
  border: 1px solid var(--clr-primary);
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.card:hover {
  box-shadow: 10px 10px 0 0 var(--clr-primary);
}

.header,
.body {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.source-link {
  color: var(--clr-secondary);
}

.date {
  opacity: 0.75;
  font-weight: var(--fw-regular);
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  font-size: var(--fs-100);
}

.tag {
  --mix-color: rgba(from var(--clr-neutral-000) r g b / 0.2);
  background-color: color-mix(in srgb, currentColor 10%, var(--mix-color));
  padding: 0.125rem 0.25rem;
}

.vue {
  color: var(--clr-green);
}

.no-js {
  color: var(--clr-cyan);
}
</style>
