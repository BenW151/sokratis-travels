<template>
  <footer ref="footer">
    <LayoutGridContainer class="footer-text">
      <p>
        On a Mission to <br />
        Meet The World
      </p>

      <ButtonsRounded destination="/contact" aria-label="Go to Contact Page">
        Contact Me
      </ButtonsRounded>
    </LayoutGridContainer>
    <LayoutGridContainer class="footer">
      <div class="work-with-me">
        <FormsNewsletter />
      </div>
      <div class="location">
        <p class="subtitle">Current Location</p>
        <p class="time">
          Bali, Indonesia (CIT) <br />
          {{ currentTime }} | {{ currentDate }}
        </p>
      </div>
      <div class="nav-links">
        <ListsLinkList
          :links="[
            { url: '/', label: 'About', description: 'About Page' },
            {
              url: '/destinations',
              label: 'Destinations',
              description: 'Destinations Page',
            },
            {
              url: '/resources',
              label: 'Resources',
              description: 'Resources Page',
            },
            { url: '/contact', label: 'Contact', description: 'Contact Page' },
            {
              url: '/terms-and-conditions',
              label: 'Terms + Conditions',
              description: 'Terms + Conditions Page',
            },
            {
              url: '/privacy-policy',
              label: 'Privacy Policy',
              description: 'Privacy Policy',
            },
          ]" />
      </div>
      <div class="socials">
        <ListsLinkList
          :links="[
            {
              url: 'https://www.instagram.com/benward.io/',
              label: 'Instagram',
              description: 'Instagram',
            },
            {
              url: 'https://linkedin.com/in/benw151',
              label: 'Facebook',
              description: 'Facebook',
            },
            {
              url: 'https://github.com/BenW151',
              label: 'X',
              description: 'X',
            },
          ]" />
      </div>
      <p class="wordmark">Sokratis Travels</p>
      <div class="copyright">
        <p class="item">Copyright ©2024</p>
        <p>
          Site by
          <a
            class="underline-out"
            href="https://benward.io"
            target="_blank"
            aria-label="Link to benward.io website"
            >benward.io</a
          >
        </p>
      </div>
    </LayoutGridContainer>
  </footer>
</template>

<script setup>
import { ref, onMounted } from "vue";

const currentTime = ref("");
const currentDate = ref("");
const footer = ref(null);

const updateTime = () => {
  const optionsTime = {
    timeZone: "Asia/Makassar",
    hour: "2-digit",
    minute: "2-digit",
    second: "2-digit",
    hourCycle: "h23", // 24-hour format
  };
  const optionsDate = {
    timeZone: "Asia/Makassar",
    year: "numeric",
    month: "long",
    day: "2-digit",
  };
  const now = new Date();
  currentTime.value = now.toLocaleTimeString("en-AU", optionsTime);
  currentDate.value = now.toLocaleDateString("en-AU", optionsDate);
};

onMounted(() => {
  updateTime();
  const interval = setInterval(updateTime, 1000);

  // Initial position off-screen
  footer.value.style.position = "relative";
  footer.value.style.top = "100vh";

  // Temp fix for FOUC
  setTimeout(() => {
    footer.value.style.top = "0";
  }, 500);

  onUnmounted(() => {
    clearInterval(interval);
  });
});
</script>

<style scoped>
footer {
  width: 100%;
  height: fit-content;
  padding-bottom: 0.5vw;
  z-index: 10;
  background: var(--background-primary);
  transition: all 0.5s cubic-bezier(0.77, 0, 0.175, 1);
  background-image: url("/images/cyprus-kouklia.jpg");
}

footer .container {
  white-space: nowrap;
}

.footer-text {
  background: none;
  height: 40vw;
  color: var(--color-white);
}

.footer-text p {
  grid-column: 1 / -1;
  font-size: var(--font-size-XXL);
  font-family: var(--font-family-primary);
  line-height: 1;
  text-align: center;
  align-self: center;
  margin: 0;
}

.footer-text .rounded-button {
  grid-column: 1 / -1;
  text-align: center;
  justify-self: center;
  display: flex;
  align-items: center;
  margin: 0;
}

.footer {
  width: 99vw;
  margin-left: 0.5vw;
  margin-right: 0.5vw;
  padding-bottom: 5px;
  align-items: center;
  justify-content: space-between;
  overflow: hidden;
  background: var(--opacity-background);
  backdrop-filter: blur(3px);
  -webkit-backdrop-filter: blur(3px);
  border-radius: var(--border-radius);
}

.footer .footer-contact {
  margin-right: auto;
}

.item.active::after {
  transform: scaleX(1);
  transform-origin: bottom left;
}

.back-to-top::after {
  display: none;
}

.back-to-top:hover {
  transform: translateY(-4px);
  cursor: pointer;
}

.work-with-me {
  grid-column: 1 / 4;
  grid-row: 1;
  margin-bottom: auto;
}

.location {
  grid-column: 5 / 8;
  grid-row: 1;
  margin-bottom: auto;
}

.nav-links {
  grid-column: 9 / 12;
  grid-row: 1;
  margin-bottom: auto;
}

.socials {
  grid-column: 11 / 13;
  grid-row: 1;
  margin-bottom: auto;
}

.copyright {
  grid-column: 11 / 13;
  grid-row: 2;
  margin-top: auto;
}

.subtitle {
  font-size: var(--font-size-S);
  margin-bottom: var(--spacing-1);
}

.time {
  margin-bottom: 0;
}

.wordmark {
  grid-column: 1 / -1;
  grid-row: 2;
  transform: translateX(-0.5vw);
  font-size: var(--font-size-XXL);
  font-family: var(--font-family-primary);
  margin-bottom: 0;
}

@media (max-width: 767px) {
  footer::after {
    width: calc(100% - (2 * var(--spacing-4)));
  }

  .footer-text {
    background: none;
    height: 80vw;
  }

  .footer-text p {
    grid-column: 1 / 7;
  }

  .footer .item {
    font-size: var(--font-size-XS);
  }

  .work-with-me {
    grid-column: 1 / 7;
    grid-row: 1;
  }

  .location {
    grid-column: 1 / 7;
    grid-row: 2;
    margin-bottom: var(--spacing-4);
  }

  .nav-links {
    grid-column: 1 / 3;
    grid-row: 3;
  }

  .socials {
    grid-column: 4 / 7;
    grid-row: 3;
  }

  .copyright {
    grid-column: 4 / 7;
    grid-row: 3;
    margin-top: auto;
  }

  .wordmark {
    grid-column: 1 / 7;
    grid-row: 4;
    font-size: 12.5vw;
  }

  h5 {
    margin-bottom: 0;
  }
}

@media (min-width: 768px) and (max-width: 1024px) {
}
</style>

<style>
footer a::after,
footer button::after {
  background-color: var(--color-orange);
}
</style>
