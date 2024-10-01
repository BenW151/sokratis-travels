<template>
  <NuxtLink
    v-if="isInternalLink(destination)"
    :to="destination"
    :aria-label="ariaLabel"
    class="rounded-button"
  >
    <span class="button-text">
      <slot />
    </span>
    <span class="icon-wrapper">
      <LucideArrowUpRight class="arrow-icon" />
    </span>
  </NuxtLink>
  <a
    v-else
    :href="destination"
    :aria-label="ariaLabel"
    class="rounded-button"
    target="_blank"
    rel="noopener noreferrer"
  >
    <span class="button-text">
      <slot />
    </span>
    <span class="icon-wrapper">
      <LucideArrowUpRight class="arrow-icon" />
    </span>
  </a>
</template>

<script setup>
import { defineProps } from 'vue';
import { LucideArrowUpRight } from 'lucide-vue-next';

// Define props for destination link and aria-label
const props = defineProps({
  destination: {
    type: String,
    required: true,
  },
  ariaLabel: {
    type: String,
    required: false,
  },
});

// Function to check if the link is internal (starts with / or doesn't have http)
const isInternalLink = (url) => {
  return !url.startsWith('http');
};
</script>

<style scoped>
.rounded-button {
  display: inline-flex;
  align-items: center;
  justify-content: space-between;
  height: fit-content;
  padding: 1vw;
  border-radius: 9999px;
  background-color: var(--background-primary);
  color: var(--foreground-primary);
  text-decoration: none;
}

.rounded-button::after {
  display: none;
}

.icon-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: var(--foreground-primary);
  color: var(--background-primary);
  border-radius: 50%;
  width: 2vw;
  height: 2vw;
  margin-left: 0.5vw;
  position: relative;
}

@keyframes move-and-fade {
  0% {
    transform: translate(0, 0);
    opacity: 1;
  }
  50% {
    transform: translate(0.5em, -0.5em);
    opacity: 0;
  }
  51% {
    transform: translate(-0.5em, 0.5em);
    opacity: 0;
  }
  100% {
    transform: translate(0, 0);
    opacity: 1;
  }
}

.arrow-icon {
  color: var(--color-white);
  transition: transform 0.3s ease, opacity 0.3s ease;
}


.rounded-button:hover .arrow-icon {
  animation: move-and-fade 0.6s ease;
}

</style>
