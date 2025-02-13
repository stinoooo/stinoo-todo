<template>
  <div class="max-w-4xl mx-auto space-y-12">
    <!-- Hero Section -->
    <div class="text-center space-y-4">
      <h1 class="text-4xl font-bold bg-gradient-to-r from-cyan-400 to-blue-500 bg-clip-text text-transparent">
        Stino Todo
      </h1>
      <p class="text-xl text-slate-300">
        Simplify your life, one task at a time.
      </p>
    </div>

    <!-- Main Content -->
    <div class="space-y-8">
      <!-- App Description -->
      <div
          class="bg-slate-900/50 rounded-2xl p-8 backdrop-blur border border-slate-800
                       hover:border-slate-700 transition-all duration-300"
      >
        <h2 class="text-2xl font-semibold mb-4">About the App</h2>
        <p class="text-slate-300 leading-relaxed">
          This modern todo application is crafted with Nuxt.js 3 and Tailwind CSS,
          focusing on simplicity and efficiency. Built by Stino, it combines powerful
          features with an intuitive interface to help you stay organized.
        </p>
      </div>

      <!-- Features Grid -->
      <div class="grid sm:grid-cols-2 gap-6">
        <div
            class="group bg-slate-900/30 rounded-xl p-6 border border-slate-800/50
                           hover:border-slate-700/50 transition-all duration-300"
        >
          <div class="flex items-center gap-3 mb-3">
            <div class="p-2 rounded-lg bg-cyan-500/10 group-hover:bg-cyan-500/20 transition-colors">
              <svg class="h-5 w-5 text-cyan-400" fill="currentColor" viewBox="0 0 20 20"
                   xmlns="http://www.w3.org/2000/svg">
                <path
                    d="M5 4a1 1 0 00-2 0v7.268a2 2 0 000 3.464V16a1 1 0 102 0v-1.268a2 2 0 000-3.464V4zM11 4a1 1 0 10-2 0v1.268a2 2 0 000 3.464V16a1 1 0 102 0V8.732a2 2 0 000-3.464V4zM16 3a1 1 0 011 1v7.268a2 2 0 010 3.464V16a1 1 0 11-2 0v-1.268a2 2 0 010-3.464V4a1 1 0 011-1z"/>
              </svg>
            </div>
            <h3 class="font-semibold">Easy Customization</h3>
          </div>
          <p class="text-slate-400 group-hover:text-slate-300 transition-colors">
            Personalize your todo lists with categories, priorities, and custom tags.
          </p>
        </div>

        <div
            class="group bg-slate-900/30 rounded-xl p-6 border border-slate-800/50
                           hover:border-slate-700/50 transition-all duration-300"
        >
          <div class="flex items-center gap-3 mb-3">
            <div class="p-2 rounded-lg bg-cyan-500/10 group-hover:bg-cyan-500/20 transition-colors">
              <svg class="h-5 w-5 text-cyan-400" fill="currentColor" viewBox="0 0 20 20"
                   xmlns="http://www.w3.org/2000/svg">
                <path clip-rule="evenodd"
                      d="M11.3 1.046A1 1 0 0112 2v5h4a1 1 0 01.82 1.573l-7 10A1 1 0 018 18v-5H4a1 1 0 01-.82-1.573l7-10a1 1 0 011.12-.38z"
                      fill-rule="evenodd"/>
              </svg>
            </div>
            <h3 class="font-semibold">Lightning Fast</h3>
          </div>
          <p class="text-slate-400 group-hover:text-slate-300 transition-colors">
            Built with performance in mind, ensuring a smooth and responsive experience.
          </p>
        </div>
      </div>

      <!-- Tech Stack -->
      <div
          class="bg-slate-900/30 rounded-xl p-6 border border-slate-800/50
                       hover:border-slate-700/50 transition-all duration-300"
      >
        <h3 class="font-semibold mb-4">Built With</h3>
        <div class="flex flex-wrap gap-2">
                    <span
                        class="px-3 py-1 bg-slate-800 rounded-full text-sm text-slate-300 hover:bg-slate-700 transition-colors">
                        Nuxt.js 3
                    </span>
          <span class="px-3 py-1 bg-slate-800 rounded-full text-sm text-slate-300 hover:bg-slate-700 transition-colors">
                        Vue 3
                    </span>
          <span class="px-3 py-1 bg-slate-800 rounded-full text-sm text-slate-300 hover:bg-slate-700 transition-colors">
                        Tailwind CSS
                    </span>
          <span class="px-3 py-1 bg-slate-800 rounded-full text-sm text-slate-300 hover:bg-slate-700 transition-colors">
                        TypeScript
                    </span>
        </div>
      </div>
    </div>

    <!-- Links Section -->
    <div class="flex flex-wrap gap-4 pt-4">
      <a
          class="inline-flex items-center gap-2 px-6 py-2 font-medium text-sm text-slate-900
                       bg-gradient-to-r from-cyan-300 to-cyan-400 rounded-lg
                       transition-all duration-300 hover:shadow-lg hover:shadow-cyan-500/25
                       active:scale-95"
          href="https://github.com/stinoooo/stinoo-todo"
          rel="noreferrer noopener"
          target="_blank"
      >
        <svg aria-hidden="true" class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
          <path clip-rule="evenodd"
                d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"
                fill-rule="evenodd"/>
        </svg>
        View on GitHub
      </a>
      <a
          class="inline-flex items-center gap-2 px-6 py-2 font-medium text-sm
                       text-slate-300 border border-slate-700 rounded-lg
                       transition-all duration-300 hover:text-slate-200 hover:border-slate-600
                       hover:bg-slate-800/50"
          href="https://twitter.com/stinoooo"
          rel="noreferrer noopener"
          target="_blank"
      >
        <svg aria-hidden="true" class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
          <path
              d="M8.29 20.251c7.547 0 11.675-6.253 11.675-11.675 0-.178 0-.355-.012-.53A8.348 8.348 0 0022 5.92a8.19 8.19 0 01-2.357.646 4.118 4.118 0 001.804-2.27 8.224 8.224 0 01-2.605.996 4.107 4.107 0 00-6.993 3.743 11.65 11.65 0 01-8.457-4.287 4.106 4.106 0 001.27 5.477A4.072 4.072 0 012.8 9.713v.052a4.105 4.105 0 003.292 4.022 4.095 4.095 0 01-1.853.07 4.108 4.108 0 003.834 2.85A8.233 8.233 0 012 18.407a11.616 11.616 0 006.29 1.84"/>
        </svg>
        Follow Updates
      </a>
    </div>
  </div>
</template>

<script lang="ts" setup>
// Enhanced SEO meta tags
useSeoMeta({
  title: 'About Stino Todo',
  description: 'Learn about Stino Todo - A modern task management application built with Nuxt.js 3 and Tailwind CSS.',
  ogTitle: 'About Stino Todo',
  ogDescription: 'A modern task management application built with Nuxt.js 3 and Tailwind CSS.',
  ogType: 'website',
  twitterCard: 'summary_large_image',
  twitterTitle: 'About Stino Todo',
  twitterDescription: 'A modern task management application built with Nuxt.js 3 and Tailwind CSS.',
});

definePageMeta({
  layout: 'dashboard',
});
</script>