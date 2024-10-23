<template>
  <section>
    <LayoutGridContainer class="text-block">
      <TextSectionLabel :labelText="sectionTitle" />
      <LayoutColumn>
        <template #title
          ><h3>{{ sectionTitle }}</h3></template
        >
        <template #body>
          <div v-html="renderedMarkdown"></div>
        </template>
      </LayoutColumn>
    </LayoutGridContainer>
  </section>
</template>

<script setup>
import { computed, ref } from "vue";

const props = defineProps({
  sectionTitle: String,
  sectionText: String,
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
.text-block .column {
  grid-column: 1 / -1;
  grid-row-start: 2;
}
</style>
