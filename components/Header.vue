<template>
  <header ref="headerRef" :class="headerClass" id="header">
    <div
      class="background-color rellax"
      v-rellax
      :style="{
        backgroundColor: backgroundColor || 'var(--color-cream)',
      }"></div>
    <div
      v-if="imageUrl"
      class="background-image rellax"
      v-rellax
      data-rellax-speed="3">
      <NuxtImg format="webp" :alt="imageAlt" :src="imageUrl" preload />
    </div>
    <LayoutGridContainer>
      <div class="hero-text item">
        <h1><slot name="title"></slot></h1>
        <h2><slot name="subtitle"></slot></h2>
      </div>
    </LayoutGridContainer>
    <p class="scroll"><LucideArrowDown /> Scroll to Explore</p>
    <ListsPageIndex v-if="pageIndexLabels" :labels="pageIndexLabels" />
  </header>
</template>

<script setup>
import { onMounted, onBeforeUnmount, ref } from "vue";

const props = defineProps({
  imageUrl: String,
  imageAlt: String,
  headerClass: String,
  backgroundColor: String,
  pageIndexLabels: Array,
});

const headerRef = ref(null);

const checkScroll = () => {
  if (!headerRef.value) return;
  const header = headerRef.value;
  if (window.scrollY > header.offsetHeight) {
    document.body.classList.add("scrolled-past-header");
  } else {
    document.body.classList.remove("scrolled-past-header");
  }
  if (window.scrollY > 0) {
    document.body.classList.add("scrolled-from-top");
  } else {
    document.body.classList.remove("scrolled-from-top");
  }
};

onMounted(() => {
  window.addEventListener("scroll", checkScroll);
  checkScroll();
});

onBeforeUnmount(() => {
  window.removeEventListener("scroll", checkScroll);
});
</script>

<style scoped>
header {
  z-index: 1;
}

/* Header Size Classes */
.header-small {
  min-height: 100lvh;
  height: auto;
}
.header-medium {
  height: 120lvh;
}
.header-large {
  height: 180lvh;
}

/* Text Colors */
header,
header a,
header a .lucide {
  color: var(--foreground-primary);
}

header a.link::after {
  background-color: var(--foreground-primary);
}

.lucide {
  color: var(--background-primary);
}

/* Background Elements */
.background-color,
.background-image {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  z-index: 0;
}

.background-color {
  background-color: var(--color-cream);
}

.background-image img {
  height: 120lvh;
  width: 100%;
  object-fit: cover;
  object-position: 50% 50%;
  filter: brightness(0.7);
}

/* Scroll Indicator */
.scroll,
.page-index {
  position: absolute;
  bottom: var(--spacing-4);
  z-index: 100;
  margin: 0;
  display: flex;
  align-items: center;
  opacity: var(--opacity);
}

.scroll {
  left: var(--spacing-5);
  color: var(--background-primary);
  font-size: var(--font-size-XXS);
}

body.scrolled-from-top .scroll {
  opacity: 0;
}

/* Hero Text */
.container {
  height: 100lvh;
  background: none;
}

.hero-text {
  grid-column: 1 / -1;
  grid-row-start: 1;
  align-self: center;
  color: var(--color-white);
}

.hero-text h2 {
  font-family: var(--font-family-primary);
  font-size: var(--font-size-M);
  text-align: center;
}

.hero-text h3 {
  font-size: var(--font-size-S);
}

@media (max-width: 767px) {
  .header-small {
    height: 100svh;
  }
  .header-medium {
    height: 110lvh;
  }
  .header-large {
    height: 130lvh;
  }

  .background-image img {
    height: 110lvh;
    object-position: 50% 50%;
  }

  .hero-text {
    grid-column: span 6;
    grid-row-start: 1;
  }

  .scroll {
    display: none;
  }

  .page-index {
    font-size: var(--font-size-XS);
    right: 0;
    width: 100%;
  }
}
</style>

<style>
.hero-text .line-container,
.hero-text .text-reveal {
  justify-content: center;
}
</style>
