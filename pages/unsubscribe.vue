<template>
  <div>
    <Header
      imageUrl="/images/denmark-cover.png"
      imageAlt="View of Rakaposhi from Karimabad"
      headerClass="header-small">
      <template #title> Unsubscribe </template>
      <template #subtitle> Enter Your Email Below. </template>
    </Header>

    <div class="unsubscribe">
      <section id="unsubscribe">
        <LayoutGridContainer>
          <FormsNewsletterUnsubscribe />
        </LayoutGridContainer>
      </section>
    </div>
  </div>
</template>

<script setup>
useHead({
  title: "Unsubscribe | Sokratis Travels",
  meta: [
    {
      name: "description",
      content: "Unsubscribe From Our Mailing List.",
    },
    {
      hid: "robots",
      name: "robots",
      content: "noindex",
    },
  ],
  link: [
    {
      rel: "canonical",
      href: "https://sokratistravels.com/unsubscribe",
    },
  ],
});
</script>

<style scoped>
#unsubscribe .item.newsletter {
  grid-column: 6 / 12;
  grid-row: 1;
}

@media (max-width: 767px) {
  #unsubscribe .item.newsletter {
    grid-column: 1 / 7;
    grid-row: auto;
    margin-top: 6vh;
  }
}
</style>
