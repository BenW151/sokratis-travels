<template>
  <div class="contact">
    <Header
      imageUrl="/images/denmark-cover.png"
      imageAlt="Attabad Lake"
      headerClass="header-small">
      <template #title> Contact </template>
      <template #subtitle> Have a question? Let us know </template>
    </Header>

    <section id="contact-form">
      <FormsContactForm />
    </section>
  </div>
</template>

<script setup>
useHead({
  title: "Contact | Sokratis Travels",
  meta: [
    {
      name: "description",
      content: "Get in Touch: We're Here to Help Plan Your Next Adventure.",
    },
  ],
  link: [
    {
      rel: "canonical",
      href: "https://sokratistravels.com/contact",
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
            name: "Contact",
            item: "https://sokratistravels.com/contact",
          },
        ],
      }),
    },
  ],
});
</script>

<style>
.contact header .item.paragraph:nth-child(2) {
  grid-column: 15 / 16;
}
</style>
