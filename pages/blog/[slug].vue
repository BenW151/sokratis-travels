<template>
  <div class="blog">
    <!-- Placeholder Header (visible when content is loading) -->
    <Header
      v-if="!contentLoaded"
      backgroundColor="var(--background-primary)"
      title=""
      subtitle=""
      headerClass="header-small" />

    <!-- Blog Content -->
    <ContentDoc v-slot="{ doc }">
      <article v-if="contentLoaded">
        <!-- Actual Header -->
        <Header
          :imageUrl="doc.headerImageUrl"
          :imageAlt="doc.headerImageAlt"
          headerClass="header-small">
          <template #title>
            {{ doc.title }}
          </template>
          <template #subtitle>
            {{ doc.subtitle }}
          </template>
        </Header>

        <section class="text-left">
          <LayoutGridContainer>
            <TextSectionLabel :labelText="doc.sectionOneTitle" />
            <LayoutColumn subtitleTag="h3">
              <template #title>{{ doc.sectionOneTitle }}</template>
              <template #body>
                <p v-html="doc.sectionOneText"></p>
              </template>
            </LayoutColumn>
            <ImageWithTextOverlay
              :imageUrl="doc.sectionOneImageUrl"
              :imageAlt="doc.sectionOneImageAlt"
              :overlayText="doc.sectionOneImageAlt"
              textPosition="right" />
          </LayoutGridContainer>
        </section>

        <section class="text-right">
          <LayoutGridContainer>
            <TextSectionLabel :labelText="doc.sectionTwoTitle" />
            <LayoutColumn subtitleTag="h3">
              <template #title>{{ doc.sectionTwoTitle }}</template>
              <template #body>
                <p v-html="doc.sectionTwoText"></p>
              </template>
            </LayoutColumn>
            <ImageWithTextOverlay
              :imageUrl="doc.sectionTwoImageUrl"
              :imageAlt="doc.sectionTwoImageAlt"
              :overlayText="doc.sectionTwoImageAlt"
              textPosition="left" />
          </LayoutGridContainer>
        </section>

        <section class="text-left">
          <LayoutGridContainer>
            <TextSectionLabel :labelText="doc.sectionThreeTitle" />
            <LayoutColumn subtitleTag="h3">
              <template #title>{{ doc.sectionThreeTitle }}</template>
              <template #body>
                <p v-html="doc.sectionThreeText"></p>
              </template>
            </LayoutColumn>
            <ImageWithTextOverlay
              :imageUrl="doc.sectionThreeImageUrl"
              :imageAlt="doc.sectionThreeImageAlt"
              :overlayText="doc.sectionThreeImageAlt"
              textPosition="right" />
          </LayoutGridContainer>
        </section>

        <section class="text-right">
          <LayoutGridContainer>
            <TextSectionLabel :labelText="doc.sectionFourTitle" />
            <LayoutColumn subtitleTag="h3">
              <template #title>{{ doc.sectionFourTitle }}</template>
              <template #body>
                <p v-html="doc.sectionFourText"></p>
              </template>
            </LayoutColumn>
            <ImageWithTextOverlay
              :imageUrl="doc.sectionFourImageUrl"
              :imageAlt="doc.sectionFourImageAlt"
              :overlayText="doc.sectionFourImageAlt"
              textPosition="left" />
          </LayoutGridContainer>
        </section>

        <BlogRelatedPosts labelText="Related Posts">
          <template #title>Related Posts</template>
          <template #body>
            <p>
              Explore the countries I've had the pleasure of visiting. Each
              destination has its own unique character and charm, offering a
              diverse range of experiences and stories. Click through to read
              about my adventures in these places, discover local tips, and see
              the highlights of each country I've explored. I hope my travels
              inspire your own journey to these amazing locations!
            </p>
          </template>
        </BlogRelatedPosts>
      </article>
    </ContentDoc>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const contentLoaded = ref(false);

onMounted(() => {
  setTimeout(() => {
    contentLoaded.value = true;
  }, 200);
});
</script>

<style scoped>
.blog-text {
  grid-column: 5 / 13;
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
  grid-column: 7 / 13;
  grid-row-start: 2;
}

.text-right .image {
  grid-column: 1 / 6;
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

<style>
.blog .paragraph.medium {
  display: none;
}
</style>
