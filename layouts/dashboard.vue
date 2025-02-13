<template>
  <div class="min-h-screen flex flex-col bg-slate-950">
    <!-- Navigation -->
    <nav
        class="sticky top-0 w-full z-50 backdrop-blur-lg border-b border-slate-800/50"
    >
      <div class="bg-gradient-to-b from-slate-900/90 to-slate-950/90">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8">
          <div class="flex items-center justify-between h-16">
            <!-- Left side - Brand and primary navigation -->
            <div class="flex items-center gap-8">
              <!-- Brand -->
              <NuxtLink
                  class="flex items-center gap-2 font-medium text-lg tracking-tight hover:text-cyan-300 transition-colors"
                  to="/"
              >
                <!-- Logo/Icon -->
                <div
                    class="w-8 h-8 rounded-lg bg-gradient-to-br from-cyan-400 to-blue-500 flex items-center justify-center shadow-lg shadow-cyan-500/20">
                  <svg class="h-5 w-5 text-white" fill="currentColor" viewBox="0 0 20 20"
                       xmlns="http://www.w3.org/2000/svg">
                    <path d="M9 2a1 1 0 000 2h2a1 1 0 100-2H9z"/>
                    <path clip-rule="evenodd"
                          d="M4 5a2 2 0 012-2 3 3 0 003 3h2a3 3 0 003-3 2 2 0 012 2v11a2 2 0 01-2 2H6a2 2 0 01-2-2V5zm9.707 5.707a1 1 0 00-1.414-1.414L9 12.586l-1.293-1.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z"
                          fill-rule="evenodd"/>
                  </svg>
                </div>
                Todo App
              </NuxtLink>

              <!-- Primary Navigation -->
              <div class="hidden sm:flex items-center gap-6">
                <NuxtLink
                    v-for="item in navigationItems"
                    :key="item.path"
                    :class="[
                                        route.path === item.path
                                            ? 'text-cyan-300'
                                            : 'text-slate-400 hover:text-slate-200',
                                    ]"
                    :to="item.path"
                    class="relative text-sm font-medium px-1 py-2 transition-colors"
                >
                  {{ item.name }}
                  <!-- Active indicator -->
                  <div
                      v-if="route.path === item.path"
                      class="absolute bottom-0 left-0 w-full h-0.5 bg-cyan-300 rounded-full"
                  />
                </NuxtLink>
              </div>
            </div>

            <!-- Right side - Theme toggle and mobile menu -->
            <div class="flex items-center gap-4">
              <!-- Theme Toggle -->
              <button
                  aria-label="Toggle theme"
                  class="p-2 text-slate-400 hover:text-slate-200 transition-colors"
                  @click="toggleTheme"
              >
                <svg class="h-5 w-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                  <path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z"/>
                </svg>
              </button>

              <!-- Mobile menu button -->
              <button
                  :aria-expanded="isMobileMenuOpen"
                  aria-label="Toggle mobile menu"
                  class="sm:hidden p-2 text-slate-400 hover:text-slate-200 transition-colors"
                  @click="isMobileMenuOpen = !isMobileMenuOpen"
              >
                <svg
                    class="h-6 w-6"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                      v-if="!isMobileMenuOpen"
                      d="M4 6h16M4 12h16M4 18h16"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                  />
                  <path
                      v-else
                      d="M6 18L18 6M6 6l12 12"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                  />
                </svg>
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- Mobile menu -->
      <Transition
          enter-active-class="transition duration-200 ease-out"
          enter-from-class="transform -translate-y-2 opacity-0"
          enter-to-class="transform translate-y-0 opacity-100"
          leave-active-class="transition duration-150 ease-in"
          leave-from-class="transform translate-y-0 opacity-100"
          leave-to-class="transform -translate-y-2 opacity-0"
      >
        <div
            v-show="isMobileMenuOpen"
            class="sm:hidden bg-slate-900/95 border-b border-slate-800/50"
        >
          <div class="container mx-auto px-4 py-3 space-y-1">
            <NuxtLink
                v-for="item in navigationItems"
                :key="item.path"
                :class="[
                                route.path === item.path
                                    ? 'bg-cyan-500/10 text-cyan-300'
                                    : 'text-slate-400 hover:bg-slate-800 hover:text-slate-200',
                            ]"
                :to="item.path"
                class="block px-3 py-2 rounded-md text-base font-medium transition-colors"
                @click="isMobileMenuOpen = false"
            >
              {{ item.name }}
            </NuxtLink>
          </div>
        </div>
      </Transition>
    </nav>

    <!-- Main content -->
    <main class="container mx-auto px-4 sm:px-6 lg:px-8 py-8 flex-1">
      <slot/>
    </main>
  </div>
</template>

<script lang="ts" setup>
const route = useRoute();
const isMobileMenuOpen = ref(false);

// Navigation items
const navigationItems = [
  {name: 'Tasks', path: '/'},
  {name: 'About', path: '/about'},
];

// Theme toggle (placeholder for now)
const toggleTheme = () => {
  // Implement theme toggle functionality
  console.log('Theme toggle clicked');
};

// Close mobile menu when route changes
watch(
    () => route.path,
    () => {
      isMobileMenuOpen.value = false;
    }
);

// Close mobile menu when clicking outside
onMounted(() => {
  const handleClickOutside = (event: MouseEvent) => {
    const target = event.target as HTMLElement;
    if (isMobileMenuOpen.value && !target.closest('nav')) {
      isMobileMenuOpen.value = false;
    }
  };

  document.addEventListener('click', handleClickOutside);
  onUnmounted(() => {
    document.removeEventListener('click', handleClickOutside);
  });
});

// Handle escape key
onMounted(() => {
  const handleEscape = (event: KeyboardEvent) => {
    if (event.key === 'Escape' && isMobileMenuOpen.value) {
      isMobileMenuOpen.value = false;
    }
  };

  document.addEventListener('keydown', handleEscape);
  onUnmounted(() => {
    document.removeEventListener('keydown', handleEscape);
  });
});
</script>