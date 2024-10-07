<template>
  <div class="destination-pages">
    <Header
      imageUrl="/images/denmark-cover.png"
      imageAlt="TODO alt"
      headerClass="header-small">
      <template #title> Europe </template>
      <template #subtitle> Explore Posts by Destination. </template>
    </Header>

    <BlogCountryPosts region="europe" />

    <BlogRegionalDestinations region="europe" />
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

<style scoped>
.country-posts-text .container {
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

@media (max-width: 767px) {
  section div.container.grid div.item,
  .end-text a {
    grid-column: 1 / 7;
    grid-row: auto;
  }

  .container .image:nth-of-type(2) {
    height: 40vh;
  }
}
</style>
