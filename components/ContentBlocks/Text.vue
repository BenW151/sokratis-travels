<template>
  <section>
    <LayoutGridContainer class="text-block">
      <TextSectionLabel :labelText="sectionTitle" />
      <LayoutColumn>
        <template #title><h3>{{ sectionTitle }}</h3></template>
        <template #body>
          <div>
            <p v-for="(paragraph, index) in paragraphs" :key="index" v-html="paragraph"></p>
          </div>
        </template>
      </LayoutColumn>
    </LayoutGridContainer>
  </section>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  sectionTitle: String,
  sectionText: String,
});

const paragraphs = computed(() => {
  return props.sectionText
    ? props.sectionText.split(/\n\s*\n/).filter(p => p.trim() !== '')
    : [];
});
</script>

<style scoped>
.text-block .column {
  grid-column: 1 / -1;
  grid-row-start: 2;
}
</style>
