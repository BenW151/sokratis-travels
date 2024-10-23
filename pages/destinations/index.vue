<template>
  <div class="destination-pages">
    <Header
      imageUrl="/images/denmark-cover.png"
      imageAlt="TODO alt"
      headerClass="header-small">
      <template #title> Destinations </template>
      <template #subtitle> Explore Posts by Destination. </template>
    </Header>

    <BlogRegions />

    <BlogDestinationItems labelText="Countries">
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
    </BlogDestinationItems>
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
      href: "https://sokratistravels.com/destinations",
    },
  ],
  script: [
    {
      type: "application/ld+json",
      innerHTML: JSON.stringify({
        "@context": "https://schema.org",
        "@type": "BreadcrumbList",
        itemListElement: [
          {
            "@type": "ListItem",
            position: 1,
            name: "Home",
            item: "https://sokratistravels.com/",
          },
          {
            "@type": "ListItem",
            position: 2,
            name: "Destinations",
            item: "https://sokratistravels.com/destinations",
          },
        ],
      }),
    },
  ],
});
</script>

<style scoped></style>

<style>
.destination-pages .paragraph.medium {
  display: none;
}
</style>
