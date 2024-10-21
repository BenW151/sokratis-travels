<template>
  <div class="column">
    
    <template v-if="useTextReveal">
      <TextReveal>
        <div class="subtitle">
          <slot name="title"></slot>
        </div>
      </TextReveal>
    </template>

    <template v-else>
      <slot name="title" class="subtitle"></slot>
    </template>

    <slot name="body" class="body"> </slot>
  </div>
</template>

<script setup>
const props = defineProps({
  useTextReveal: {
    type: Boolean,
    default: false, // Use TextReveal by default
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
