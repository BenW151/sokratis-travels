<template>
  <div class="destination-pages">
    <Header
      imageUrl="/images/jordan-cover.png"
      imageAlt="TODO alt"
      headerClass="header-small">
      <template #title> Middle East </template>
      <template #subtitle> Explore Posts by Destination. </template>
    </Header>

    <BlogCountryPosts region="middle-east" labelText="Blog Posts">
      <template #title>Blog Posts</template>
      <template #body>
        <p>
          Here, you'll find a collection of my latest travel adventures,
          insights, and personal stories from the road. Each post is a
          reflection of my experiences and discoveries, offering tips,
          recommendations, and a glimpse into the places I've explored. Dive in
          and join me as I share the highs and lows of my travels, and
          hopefully, inspire your own adventures along the way.
        </p>
      </template>
    </BlogCountryPosts>

    <BlogRegionalDestinations region="middle-east" labelText="Countries">
      <template #title>Countries</template>
      <template #body>
        <p>
          Explore the countries I've had the pleasure of visiting. Each
          destination has its own unique character and charm, offering a diverse
          range of experiences and stories. Click through to read about my
          adventures in these places, discover local tips, and see the
          highlights of each country I've explored. I hope my travels inspire
          your own journey to these amazing locations!
        </p>
      </template>
    </BlogRegionalDestinations>
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
