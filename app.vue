<template>
  <NuxtLayout>
    <NuxtPage/>
  </NuxtLayout>
</template>

<script setup lang="ts">
const image = new URL("/open-graph.png", useRequestURL());

// Enhanced SEO configuration
useSeoMeta({
  titleTemplate: (titleChunk) => {
    return titleChunk ? `${titleChunk} - Todo App` : "Todo App";
  },
  description: "A Simple Todo app",

  // Open Graph
  ogTitle: "Todo App",
  ogDescription: "A Simple Todo app",
  ogType: "website",
  ogImage: image.toString(),
  ogImageWidth: 900,
  ogImageHeight: 473,
  ogImageAlt: "Todo App",

  // Twitter Card
  twitterCard: "summary_large_image",
  twitterTitle: "Todo App",
  twitterDescription: "A Simple Todo app",
  twitterImage: image.toString(),

  // Additional meta tags
  themeColor: "#0891b2", // Cyan-600 for theme color
  viewport: "width=device-width, initial-scale=1, maximum-scale=1",
  colorScheme: "dark",

  // Application info
  applicationName: "Todo App",
  author: "Stino",
});

// Add error handling for the image URL
onMounted(() => {
  const img = new Image();
  img.onerror = () => {
    console.warn('Open Graph image failed to load:', image.toString());
  };
  img.src = image.toString();
});
</script>

<style>
/* Ensure proper height behavior */
html,
body,
#__nuxt {
  height: 100%;
}

/* Smooth scrolling */
html {
  scroll-behavior: smooth;
}
</style>