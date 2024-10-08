<template>
  <NuxtLink
    v-if="isInternalLink(destination)"
    :to="destination"
    :aria-label="ariaLabel"
    :class="['rounded-button', { dark: darkMode }]">
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
    :class="['rounded-button', { dark: darkMode }]"
    target="_blank"
    rel="noopener noreferrer">
    <span class="button-text">
      <slot />
    </span>
    <span class="icon-wrapper">
      <LucideArrowUpRight class="arrow-icon" />
    </span>
  </a>
</template>

<script setup>
import { defineProps } from "vue";
import { LucideArrowUpRight } from "lucide-vue-next";

// Define props for destination, aria-label, and darkMode
const props = defineProps({
  destination: {
    type: String,
    required: true,
  },
  ariaLabel: {
    type: String,
    required: false,
  },
  darkMode: {
    type: Boolean,
    default: false, // Default to light mode
  },
});

// Function to check if the link is internal (starts with / or doesn't have http)
const isInternalLink = (url) => {
  return !url.startsWith("http");
};
</script>

<style scoped>
.rounded-button {
  display: inline-flex;
  align-items: center;
  justify-content: space-between;
  height: 3vw;
  padding: 0.5vw;
  padding-left: 1vw;
  border-radius: 9999px;
  background-color: var(--background-primary);
  color: var(--foreground-primary);
  text-decoration: none;
}

.rounded-button.dark {
  background-color: var(--color-green); /* Swap colors for dark mode */
  color: var(--background-primary);
}

.icon-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: var(--color-green);
  color: var(--background-primary);
  border-radius: 50%;
  width: 0vw;
  height: 0vw;
  margin-left: 0.5vw;
  position: relative;
}

.rounded-button.dark .icon-wrapper {
  background-color: var(--background-primary); /* Swap colors for dark mode */
  color: var(--color-green);
}

.rounded-button.dark .lucide {
  color: var(--color-green);
}

.rounded-button::after {
  display: none;
}

@keyframes move-and-fade {
  0% {
    transform: translate(-0.5em, 0.5em);
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

.rounded-button:hover .icon-wrapper {
  width: 2vw;
  height: 2vw;
}

@media (max-width: 767px) {
  .rounded-button {
    padding: 1.5vw;
    padding-left: 3vw;
    border-radius: 9999px;
    height: fit-content;
  }

  .icon-wrapper {
    width: 5vw;
    height: 5vw;
    margin-left: 1.5vw;
  }

  .rounded-button:hover .icon-wrapper {
    width: 5vw;
    height: 5vw;
  }
}
</style>
