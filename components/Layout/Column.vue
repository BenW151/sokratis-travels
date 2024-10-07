<template>
  <div class="item column">
    <!--<div :class="[textPosition]">-->
      <component :is="subtitleTag" class="subtitle">
        <template v-if="useTextReveal">
          <TextReveal>
            <slot name="title"></slot>
          </TextReveal>
        </template>
        <template v-else>
          <slot name="title"></slot>
        </template>
      </component>

      <slot name="body">
        <p class="body">Default paragraph content.</p>
      </slot>
   <!-- </div>-->
  </div>
</template>

<script setup>
const props = defineProps({
  subtitleTag: {
    type: String,
    default: "h3",
  },
  useTextReveal: {
    type: Boolean,
    default: false, // Use TextReveal by default
  },
  textPosition: {
    type: String,
    default: "left",
  },
});
</script>

<style scoped>
.column {
  grid-column: span 7;
  margin: auto;
  z-index: 5;
}

.item-inner {
  margin: var(--spacing-4);
}

.item-inner.right {
  margin-right: 0;
}

.item-inner.left {
  margin-left: 0;
}

@media (max-width: 767px) {
  .column {
    grid-column: span 6;
  }

  .item-inner {
    margin: 0;
  }
}
</style>
