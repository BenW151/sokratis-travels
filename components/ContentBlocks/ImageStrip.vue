<template>
  <section class="image-layover">
    <LayoutGridContainer>
      <div
        class="background-image no-transition"
        :style="{ backgroundImage: `url(${imageUrl})` }"
        :title="altText"
        ref="backgroundImageRef"></div>
    </LayoutGridContainer>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";
import { useNuxtApp } from "#app";

const props = defineProps({
  imageUrl: {
    type: String,
    required: true,
  },
  altText: {
    type: String,
    default: '',
  },
});

const backgroundImageRef = ref(null);

const { $gsap } = useNuxtApp();

onMounted(() => {
  // Parallax effect for the background image
  if (backgroundImageRef.value) {
    $gsap.to(backgroundImageRef.value, {
      yPercent: 20,
      ease: "none",
      scrollTrigger: {
        trigger: backgroundImageRef.value,
        start: "top bottom",
        end: "bottom top",
        scrub: true,
      },
    });
  }
});

onBeforeUnmount(() => {
  // Clean up GSAP animations
  $gsap.killTweensOf(backgroundImageRef.value);
  $gsap.globalTimeline.clear();
});
</script>


<style scoped>
.image-layover {
  position: relative;
  overflow: hidden;
  height: 50vw;
}

.container {
  height: 100%;
}

.background-image {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 120%;
  background-size: cover;
  background-repeat: no-repeat;
  will-change: transform;
}

@media (max-width: 767px) {
  .image-1,
  .image-2 {
    grid-column: 1 / 7;
  }

  .image-layover {
    height: 100vw;
  }
}
</style>
