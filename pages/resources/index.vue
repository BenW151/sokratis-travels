<template>
  <div class="resources">
    <Header
      imageUrl="/images/denmark-cover.png"
      imageAlt="TODO alt"
      headerClass="header-small">
      <template #title> Resources </template>
      <template #subtitle> Helpful Resources. </template>
    </Header>

    <ItemGridItems labelText="Resources">
      <template #title>Resources</template>
      <template #body>
        <p>
          Here are some of my favourite resources to help you make the most of
          your travels. From must-have gear to essential tips and tricks, I've
          gathered everything you need to prepare for your adventures. Whether
          you're looking for packing advice, destination guides, or travel
          hacks, these resources are designed to make your journey smoother and
          more enjoyable. Explore my recommendations and get ready to travel
          like a pro!
        </p>
      </template>
      <ItemGridItem
        itemUrl="/resources/travel-gear"
        itemImage="/images/hiking-bag.png"
        itemImageAlt="Image 1 description"
        itemLabel="Travel Gear"
        itemDescription="Recommended Travel Gear." />
      <ItemGridItem
        itemUrl="/resources/travel-resources"
        itemImage="/images/map.png"
        itemImageAlt="Image 1 description"
        itemLabel="Travel Resources"
        itemDescription="How I Plan My Trips." />
      <ItemGridItem
        itemUrl="/resources/travel-resources"
        itemImage="/images/argentina-cover.png"
        itemImageAlt="Image 1 description"
        itemLabel="Earning Money Abroad"
        itemDescription="How I Plan My Trips." />
    </ItemGridItems>
  </div>
</template>

<script setup>
useHead({
  title: "Sokratis Travels | Destinations",
  meta: [
    {
      name: "description",
      content:
        "Providing professional web development services focused on creating modern, responsive, and user-friendly websites tailored to your needs.",
    },
  ],
  link: [
    {
      rel: "canonical",
      href: "https://benward.io/",
    },
  ],
});
</script>

<style scoped></style>

<style>
.resources-text .container {
  padding-bottom: 0;
}

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
  grid-column: 9 / 13;
  grid-row-start: 2;
}

.text-right .image {
  grid-column: 1 / 8;
  grid-row-start: 2;
  height: 40vw;
}
</style>
