<template>
  <div class="index">
    <Header
      imageUrl="/images/larnaca.jpg"
      imageAlt="View of Rakaposhi from Karimabad"
      imageLocation="34.9182° N, 33.6201° E"
      headerClass="header-small">
      <template #title>
        On a <span class="underline">Mission</span> to <br />
        Meet the World
      </template>
      <template #subtitle> Sokratis Travels </template>
    </Header>

    <main>
      <section class="lead-text">
        <LayoutGridContainer>
          <TextColorOnScroll tag="h3" class="item">
            Get ready to explore the world like never before with Sokratis
            Travels. Dive into our travel stories and uncover the essence of
            each destination through unique experiences and insider tips.
          </TextColorOnScroll>
        </LayoutGridContainer>
      </section>

      <section class="about text-left">
        <LayoutGridContainer>
          <TextSectionLabel labelText="About" />
          <LayoutColumn>
            <template #title><h3>Start Planning Your Trip</h3></template>
            <template #body>
              <p>
                Ready to turn your travel dreams into reality? Whether you're
                seeking thrilling adventures, serene escapes, or cultural
                immersions, we're here to help you every step of the way.
                Explore our curated guides, travel tips, and destination
                highlights to begin crafting your perfect itinerary. From
                finding the best local experiences to navigating must-see
                landmarks, Sokratis Travels provides all the inspiration and
                information you need to plan an unforgettable journey. Start
                your adventure today and let the world be your playground!
              </p>
              <ButtonsRounded
                destination="/resources"
                aria-label="Go to Resources Page"
                :darkMode="true">
                View Travel Resources
              </ButtonsRounded>
            </template>
          </LayoutColumn>
          <ImageWithTextOverlay
            imageUrl="/images/denmark-cover.png"
            imageAlt="Copenhagen, Denmark"
            overlayText="Copenhagen, <br /> Denmark"
            textPosition="right" />
        </LayoutGridContainer>
      </section>

      <BlogRegions labelText="Destinations"/>

      <section class="profile text-right">
        <LayoutGridContainer>
          <TextSectionLabel labelText="Profile" />
          <LayoutColumn>
            <template #title><h3>Who Am I?</h3></template>
            <template #body>
              <p>
                Hi, I'm Tia, your guide to the world's most exciting
                destinations. With a passion for travel and a love for
                discovering hidden gems, I've dedicated myself to sharing my
                journeys with you. From navigating bustling streets to relaxing
                in serene spots, my experiences offer a personal touch to each
                destination I visit. Join me as I explore new places, embrace
                local cultures, and uncover the stories that make each adventure
                unique. Let's travel the world together!
              </p>
              <ButtonsRounded
                destination="https://instagram.com/teetravels_"
                aria-label="Go to Instagram"
                :darkMode="true">
                View Instagram
              </ButtonsRounded>
            </template>
          </LayoutColumn>
          <ImageWithTextOverlay
            imageUrl="/images/sokratis-diving.jpg"
            imageAlt="Passu Cones, Pakistan"
            overlayText="Passu Cones, <br /> Pakistan"
            textPosition="left" />
        </LayoutGridContainer>
      </section>
    </main>
  </div>
</template>

<script setup>
useHead({
  title: "Sokratis Travels",
  meta: [
    {
      name: "description",
      content:
        "Sokratis Travels offers affordable tours to off the beaten track destinations, delivering expertly crafted itineraries and authentic adventures.",
    },
  ],
  link: [
    {
      rel: "canonical",
      href: "https://whynotadventures.co.uk",
    },
  ],
});

const { windowWidth, isMobile } = useWindowWidth();
</script>

<style scoped>
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
  grid-column: 7 / 13;
  grid-row-start: 2;
}

.text-right .image {
  grid-column: 1 / 6;
  grid-row-start: 2;
  height: 40vw;
}

.destinations .column {
  grid-column: 1 / 7;
  grid-row: 2;
}

.faq .column:nth-of-type(1) {
  grid-column: 6 / 14;
  grid-row: 1;
}

.faq .accordion {
  grid-column: 6 / 13;
  grid-row: 2;
  /*height: 40vw;*/
}

.end-text a {
  grid-column: 6 / 13;
  grid-row: 1;
  width: fit-content;
}

.end-text a h2 {
  font-size: var(--font-size-XXL);
  margin: 0;
}

.destinations .container {
  padding-bottom: 0;
}

.carousel .container {
  padding-top: 0;
}

.lead-text .color-reveal {
  font-size: var(--font-size-M);
}

.lead-text .item,
.lead-text p {
  grid-column: 1 / -1;
}

@media (max-width: 767px) {
  .lead-text .item,
  .lead-text p {
    grid-column: 1 / 7;
    grid-row: auto;
  }

  section div.container.grid div.item,
  .end-text a {
    grid-column: 1 / 7;
    grid-row: auto;
  }

  .end-text a h2 {
    font-size: 14.5vw;
  }

  .container .image:nth-of-type(2) {
    height: 40vh;
  }
}
</style>
