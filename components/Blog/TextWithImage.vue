<template>
  <section class="text-left">
    <LayoutGridContainer>
      <TextSectionLabel :labelText="sectionTitle" />
      <LayoutColumn>
        <template #title><h3>{{ sectionTitle }}</h3></template>
        <template #body>
          <p v-html="sectionText"></p>
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
const props = defineProps({
  sectionTitle: String,
  sectionText: String,
  imageUrl: String,
  imageAlt: String
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