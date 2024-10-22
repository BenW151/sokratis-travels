<template>
  <section class="text-left">
    <LayoutGridContainer>
      <TextSectionLabel :labelText="sectionTitle" />
      <LayoutColumn>
        <template #title>
          <h3>{{ sectionTitle }}</h3>
        </template>
        <template #body>
          <!-- Render paragraphs by splitting sectionText -->
          <div>
            <p v-for="(paragraph, index) in paragraphs" :key="index" v-html="paragraph"></p>
          </div>
        </template>
      </LayoutColumn>
      <ImageWithTextOverlay
        :imageUrl="imageUrl"
        :imageAlt="imageAlt"
        :overlayText="imageAlt"
        textPosition="right" />
    </LayoutGridContainer>
  </section>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  sectionTitle: String,
  sectionText: String,
  imageUrl: String,
  imageAlt: String,
});

// Compute paragraphs by splitting sectionText by line breaks
const paragraphs = computed(() => {
  return props.sectionText
    ? props.sectionText.split(/\n\s*\n/).filter(p => p.trim() !== '')
    : [];
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
</style>