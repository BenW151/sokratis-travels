<template>
  <section :class="['itinerary-day', textPosition]" :id="dayId">
    <LayoutGridContainer>
      <TextSectionLabel
        v-if="dayId === 'day1'"
        labelText="The Plan"
        id="itinerary-detailed" />
      <h3 v-if="dayId === 'day1'" class="heading">Itinerary</h3>
      <ImageWithTextOverlay
        :imageUrl="imageUrl"
        :imageAlt="imageAlt"
        :overlayText="overlayText"
        :textPosition="imageTextPosition" />
      <LayoutColumn :subtitleTag="subtitleTag" :textPosition="textPosition">
        <template #title>{{ title }}</template>
        <template #body>
          <slot name="body"></slot>
        </template>
      </LayoutColumn>
    </LayoutGridContainer>
  </section>
</template>

<script>
export default {
  name: "ItineraryDay",
  props: {
    dayId: {
      type: String,
      required: true,
    },
    imageUrl: {
      type: String,
      required: true,
    },
    imageAlt: {
      type: String,
      required: true,
    },
    overlayText: {
      type: String,
      required: true,
    },
    textPosition: {
      type: String,
      default: "left",
      validator: (value) => ["left", "right"].includes(value),
    },
    subtitleTag: {
      type: String,
      default: "h4",
    },
    title: {
      type: String,
      required: true,
    },
  },
  computed: {
    imageTextPosition() {
      return this.textPosition === "left" ? "right" : "left";
    },
  },
};
</script>

<style scoped>
.heading {
  grid-column: 3 / 10;
  grid-row-start: 1;
}

#day1 .column,
#day1 .image {
  grid-row-start: 2;
}

.left .column {
  grid-column: 3 / 10;
  grid-row-start: 1;
}

.left .image {
  grid-column: 8 / 16;
  grid-row-start: 1;
  height: 40vw;
}

.right .column {
  grid-column: 9 / 16;
  grid-row-start: 1;
}

.right .image {
  grid-column: 3 / 11;
  grid-row-start: 1;
  height: 40vw;
}

@media (max-width: 767px) {
  .right .image,
  .left .image {
    height: 60vw;
  }

  .heading,
  #day1 .column,
  #day1 .image {
    grid-column: 1 / 7;
    grid-row-start: auto;
  }
}
</style>
