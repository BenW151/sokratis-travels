<template>
  <section v-if="mdInitialized" class="text-left content-block">
    <LayoutGridContainer>
      <TextSectionLabel :labelText="sectionLabel" />
      <LayoutColumn>
        <template #body>
          <div v-html="renderedMarkdown"></div>
        </template>
      </LayoutColumn>
      <ImageWithTextOverlay
        :imageUrl="imageUrl"
        :imageAlt="imageAlt"
        :overlayText="imageAlt"
        textPosition="right" />
    </LayoutGridContainer>
  </section>
  <div v-else>Loading content...</div>
</template>

<script setup>
import { computed, ref } from "vue";

const props = defineProps({
  sectionLabel: String,
  sectionText: String,
  imageUrl: String,
  imageAlt: String,
});

const md = ref(null);
const mdInitialized = ref(false);

(async () => {
  const MarkdownIt = (await import("markdown-it")).default;
  const markdownItSanitizer = (await import("markdown-it-sanitizer")).default;

  md.value = new MarkdownIt({
    html: false,
    linkify: true,
  }).use(markdownItSanitizer);

  mdInitialized.value = true;
})();

const renderedMarkdown = computed(() => {
  return md.value ? md.value.render(props.sectionText || "") : "";
});
</script>

<style scoped>
.text-left .column {
  grid-column: 1 / 7;
  grid-row-start: 2;
}

.text-left .image {
  grid-column: 8 / 13;
  grid-row-start: 2;
  height: 40vw;
}

.text-right .column {
  grid-column: 7 / 13;
  grid-row-start: 2;
}

.text-right .image {
  grid-column: 1 / 6;
  grid-row-start: 2;
  height: 40vw;
}

@media (max-width: 767px) {
  .text-left .column,
  .text-left .image,
  .text-right .column,
  .text-right .image {
    grid-column: 1 / -1;
    grid-row: auto;
  }

  .text-left .image,
  .text-right .image {
    height: 60vw;
  }
}
</style>
