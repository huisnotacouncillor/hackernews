<script setup lang="ts">
useServerHead({
  htmlAttrs: { lang: 'en' },
})
useSeoMeta({
  titleTemplate: 'Nuxt HN | %s',
  description: 'HackerNews clone built with Nuxt.',
  ogImage: 'https://hn.nuxt.dev/cover.jpg',
  ogImageAlt: 'Nuxt Hackernews',
  twitterImage: 'https://hn.nuxt.dev/cover.jpg',
  twitterSite: '@nuxt_js',
  twitterCreator: '@nuxt_js',
  twitterCard: 'summary_large_image',
})
</script>

<template>
  <AppHeader />
  <NuxtPage />
</template>

<style lang="postcss">
:root {
  /* Color System */
  --primary: #00DC82;
  --primary-light: #B4F4D9;
  --secondary: #020420;
  --bg-main: #F4F4F5;
  --bg-card: #FFFFFF;
  --text-primary: #020420;
  --text-secondary: #6B7280;
  
  /* Spacing System */
  --space-xs: 0.5rem;
  --space-sm: 0.75rem;
  --space-md: 1rem;
  --space-lg: 1.5rem;
  --space-xl: 2rem;

  /* Shadows */
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.12);
  --shadow-md: 0 4px 6px rgba(0,0,0,0.1);
  --shadow-lg: 0 10px 15px rgba(0,0,0,0.1);

  /* Border Radius */
  --radius-sm: 6px;
  --radius-lg: 12px;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
  font-size: 15px;
  background-color: var(--bg-main);
  margin: 0;
  padding: 0;
  color: var(--text-primary);
  overflow-y: scroll;
}

a {
  color: #020420;
  text-decoration: none;
}
.header {
  background-color: var(--secondary);
  z-index: 999;
  height: 55px;

  .inner {
    max-width: 800px;
    box-sizing: border-box;
    margin: 0px auto;
    padding: var(--space-sm) var(--space-xs);
    display: flex;
    place-items: center;
  }

  & a {
    color: var(--bg-card);
    line-height: 24px;
    transition: color 0.15s ease;
    display: inline-block;
    vertical-align: middle;
    font-weight: 300;
    letter-spacing: 0.075em;
    margin-right: var(--space-lg);

    &:hover {
      color: var(--primary);
    }

    &.active {
      color: var(--primary);
    }

    &:nth-child(6) {
      margin-right: 0;
    }
  }

  .github {
    color: #fff;
    font-size: 0.9em;
    margin: auto;
    text-align: right;
    flex-grow: 1;
    & a {
      margin-right: 0;
    }
  }
}

.logo {
  width: 30px;
  height: 30px;
  margin-right: 10px;
  display: inline-block;
  vertical-align: middle;
}

.view {
  max-width: 800px;
  margin: 0 auto;
  position: relative;
}

.appear-active {
  transition: opacity 0.4s ease;
}

.appear {
  opacity: 0;
}

@media (max-width: 860px) {
  .header .inner {
    padding: 15px 30px;
  }
}

@media (max-width: 600px) {
  .header {
    .inner {
      padding: 15px;
    }

    & a {
      margin-right: 1em;
    }

    .github {
      display: none;
    }
  }
}
</style>
