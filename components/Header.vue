<template>
  <header ref="headerRef" :class="headerClass" id="header">
    <!--<div
      ref="backgroundColorRef"
      class="background-color"
      :style="{ backgroundColor: backgroundColor || 'var(--color-cream)' }"
    ></div>-->
    <div
      ref="backgroundImageRef"
      v-if="imageUrl"
      class="background-image no-transition">
      <NuxtImg format="webp" :alt="imageAlt" :src="imageUrl" preload />
    </div>
    <LayoutGridContainer>
      <div class="hero-text item">
        <h1><slot name="title"></slot></h1>
        <h2><slot name="subtitle"></slot></h2>
      </div>
    </LayoutGridContainer>
    <p class="scroll"><LucideArrowDown /> Scroll to Explore</p>
    <p v-if="imageLocation" class="location">
      <LucideCompass /> {{ imageLocation }}
    </p>
    <!--<ListsPageIndex v-if="pageIndexLabels" :labels="pageIndexLabels" />-->
  </header>
</template>

<script setup>
import { onMounted, onBeforeUnmount, ref } from "vue";
import { useNuxtApp } from "#app";

const props = defineProps({
  imageUrl: String,
  imageAlt: String,
  imageLocation: String,
  headerClass: String,
  backgroundColor: String,
  pageIndexLabels: Array,
});

const { $gsap } = useNuxtApp();

const headerRef = ref(null);
const backgroundImageRef = ref(null);
const backgroundColorRef = ref(null);

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

  // Parallax effect for the background image
  $gsap.to(backgroundImageRef.value, {
    yPercent: 15,
    ease: "none",
    scrollTrigger: {
      trigger: headerRef.value,
      start: "top top",
      end: "bottom top",
      scrub: true,
    },
  });
});

onBeforeUnmount(() => {
  window.removeEventListener("scroll", checkScroll);
  $gsap.killTweensOf([backgroundImageRef.value, backgroundColorRef.value]);
  $gsap.globalTimeline.clear();
});
</script>

<style scoped>
header {
  position: relative;
  overflow: hidden;
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
  position: absolute;
  top: 0;
  left: 0;
  z-index: 0;
  will-change: transform;
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
.page-index,
.location {
  position: absolute;
  bottom: var(--spacing-4);
  z-index: 100;
  margin: 0;
  display: flex;
  align-items: center;
  opacity: var(--opacity);
  font-size: var(--font-size-XS);
  color: var(--background-primary);
}

.scroll {
  left: var(--spacing-5);
}

.location {
  right: var(--spacing-5);
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
