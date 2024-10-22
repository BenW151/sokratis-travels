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
          :imageLocation="doc.headerImageLocation"
          headerClass="header-small">
          <template #title>
            {{ doc.title }}
          </template>
          <template #subtitle>
            {{ doc.subtitle }}
          </template>
        </Header>

        <!-- Render content blocks dynamically -->
        <div v-for="(block, index) in doc.content_blocks" :key="index">
          <!-- Dynamically load the correct component for each block type -->
          <component
            :is="getComponent(block.type)"
            v-bind="block"
          />
        </div>

        <!-- Related Posts Section -->
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
import ContentBlockTextWithImage from '~/components/ContentBlocks/TextWithImage.vue'; // Import your component
import ContentBlockText from '~/components/ContentBlocks/Text.vue'; // Import your component
import ContentBlockImageStrip from '~/components/ContentBlocks/ImageStrip.vue'; // Import your component

const contentLoaded = ref(false);

onMounted(() => {
  setTimeout(() => {
    contentLoaded.value = true;
  }, 200);
});

// Function to determine which component to render for each block type
const getComponent = (type) => {
  switch (type) {
    case 'text_with_image':
      return ContentBlockTextWithImage;
    case 'text':
      return ContentBlockText;
    case 'image_strip':
      return ContentBlockImageStrip;
    default:
      return null;
  }
};
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
