<template>
  <header ref="headerRef" :class="headerClass" id="header">
    <div
      class="background-color rellax"
      v-rellax
      style="background: var(--color-cream);"></div>
    <div
      v-if="imageUrl"
      class="background-image rellax"
      v-rellax
      data-rellax-speed="3">
      <NuxtImg format="webp" :alt="imageAlt" :src="imageUrl" preload />
    </div>
    <div
      v-else
      v-rellax
      :style="{ backgroundColor: backgroundColor }"
      class="background-color rellax"></div>
    <LayoutGridContainer>
      <div class="hero-text item">
        <h1><slot name="title"></slot></h1>
        <h2><slot name="subtitle"></slot></h2>
      </div>
    </LayoutGridContainer>
    <p class="scroll"><LucideArrowDown /> Scroll</p>
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

header,
header a,
header a .lucide {
  color: var(--foreground-primary);
}

header a.link::after {
  background-color: var(--foreground-primary);
}

.container {
  min-height: 100lvh;
}

.background-image {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  z-index: 0;
  pointer-events: none;
}

.index .background-image {
  top: 13vw;
  z-index: 1;
}

.background-image img {
  height: 120lvh;
  width: 100%;
  object-fit: cover;
  object-position: 50% 50%;
  top: 0;
  bottom: 0;
  right: 0;
  filter: brightness(0.7);
}

.background-color {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  z-index: 0;
}

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
}

.scroll,
.scroll .lucide {
  color: var(--background-primary);
  height: var(--font-size-XXS);
  font-size: var(--font-size-XXS);
}

.page-index {
  right: var(--spacing-5);
}

body.scrolled-from-top .scroll {
  opacity: 0;
}

.hero-text {
  grid-column: 1 / 17;
  grid-row-start: 1;
  align-self: center;
  color: var(--color-orange);
}

.hero-text h2 {
  color: var(--foreground-primary);
  font-family: var(--font-family-primary);
  font-weight: 600;
  font-size: var(--font-size-M);
  align-self: center;
  text-align: center;
}

.hero-text h3 {
  font-size: var(--font-size-S);
}

header .container {
  background: none;
}

header .item:nth-child(2) {
  grid-column: 10 / 16;
  grid-row-start: 2;
  margin-top: auto;
}

header .item:nth-child(3) {
  grid-column: 14 / 17;
  grid-row-start: 1;
  margin-top: auto;
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
    height: 60lvh;
    object-position: 80% 50%;
  }

  .hero-text {
    grid-column: span 6;
    grid-row-start: 1;
  }

  header .item:nth-child(2) {
    grid-column: 1 / 7;
    grid-row-start: 2;
    margin-top: auto;
  }

  header .item:nth-child(3) {
    grid-column: 5 / 7;
    grid-row-start: 2;
    margin-top: auto;
  }

  .scroll {
    display: none;
  }

  .page-index {
    font-size: var(--font-size-XS);
    right: 0;
    width: 100%;
  }

  .background-image img {
    height: 110lvh;
    object-position: 50% 50%;
  }

  .index .background-image {
    top: 45vh;
  }

  .index .background-image img {
    height: 60lvh;
    object-position: 80% 50%;
  }

  .index h1 {
    font-size: 26vw;
  }
}
</style>

<style>
.hero-text .line-container,
.hero-text .text-reveal {
  justify-content: center;
}
</style>
