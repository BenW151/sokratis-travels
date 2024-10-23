<template>
  <div class="blog-pages">
    <Header
      imageUrl="/images/denmark-cover.png"
      imageAlt="Laptop with code on desk"
      headerClass="header-small">
      <template #title> Recent Posts </template>
      <template #subtitle> Recent Blog Posts. </template>
    </Header>

    <BlogRecentPosts />
  </div>
</template>

<script setup>
useHead({
  title: "Sokratis Travels | Blog",
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
      href: "https://sokratistravels.com/",
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
            name: "Blog",
            item: "https://sokratistravels.com/blog",
          },
        ],
      }),
    },
  ],
});
</script>

<style scoped>
.post-title {
  font-size: var(--font-size-M);
  font-family: var(--font-family-secondary);
  margin-right: auto;
}

.post-link::after {
  display: none;
}

.post-image {
  width: 100%;
  height: 30vw;
  object-fit: cover;
}

.blog-item:nth-child(2n + 1) {
  grid-column: 1 / 7;
  grid-row: auto;
}

.blog-item:nth-child(2n) {
  grid-column: 9 / 13;
  grid-row: auto;
}

@media (max-width: 767px) {
  .post-image {
    height: 60vw;
  }

  .post-title {
    margin-bottom: 0;
  }

  .blog-item:nth-child(2n + 1) {
    grid-column: 1 / 7;
  }

  .blog-item:nth-child(2n) {
    grid-column: 1 / 7;
  }
}
</style>

<style>
.blog-pages .paragraph.medium {
  display: none;
}
</style>
