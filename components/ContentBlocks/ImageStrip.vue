<template>
  <section class="image-layover content-block">
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
import { ref, onMounted, onBeforeUnmount, watch, nextTick } from "vue";
import { useNuxtApp } from "#app";

const props = defineProps({
  imageUrl: {
    type: String,
    required: true,
  },
  altText: {
    type: String,
    default: "",
  },
});

const backgroundImageRef = ref(null);

const { $gsap } = useNuxtApp();

let gsapInitialized = false;

const initGsap = () => {
  if (gsapInitialized) return;
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
    gsapInitialized = true;
  }
};

onMounted(async () => {
  await nextTick();
  if (backgroundImageRef.value && props.imageUrl) {
    initGsap();
  } else {
    const stopWatch = watch(
      () => [backgroundImageRef.value, props.imageUrl],
      ([newRef, newImageUrl]) => {
        if (newRef && newImageUrl) {
          initGsap();
          stopWatch(); // Stop watching after initialization
        }
      }
    );
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
