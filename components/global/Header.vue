<template>
  <nav class="scrim-bg fixed z-40 top-0 inset-x-0 pt-3 px-6 flex justify-between items-center" aria-label="Main Menu">
    <a href="/" class="w-20">
      <img src="/img/dailybola.png" alt="HarianBola">
    </a>
    <div class="drawer-toggle" role="button" @click="$store.dispatch('nav/toggleSidebar')">
        <div class="bar"></div>
        <div class="bar"></div>
        <div class="bar"></div>
    </div>

    <div class="app-links">
        <AppLinks></AppLinks>
    </div>
  </nav>
</template>

<script>
import AppLinks from '~/components/global/AppLinks'
export default {
  name: 'Header',
  components: { AppLinks }
}
</script>

<style lang="postcss" scoped>
.scrim-bg {
  &::before {
    content: '';
    z-index: -1;
    background-color: var(--bg);
    @apply absolute bottom-0 inset-x-0 h-12 mb-4 transition-colors duration-200 ease-in-out;
  }
  &::after {
    content: '';
    z-index: -1;
    opacity: 1;
    animation: fadeIn1 500ms ease-in-out;
    @apply pointer-events-none absolute bottom-0 inset-x-0 h-16 -mb-12;
    background: linear-gradient(to bottom, #111827, cubic-bezier(0.15, 0, 0.45, 1), transparent);
  }
}
.nuxt-link-exact-active {
  @apply text-gray-200 border-gray-400 bg-gray-800 bg-opacity-25 cursor-default;
}

.light-mode {
  & .scrim-bg {
    &::after {
      animation-name: fadeIn2;
      background: linear-gradient(to bottom, #e5e7eb, cubic-bezier(0.15, 0, 0.45, 1), transparent);
    }
  }
  & .nuxt-link-exact-active {
    @apply text-primary-700 border-gray-600 bg-gray-100;
  }
}

/* Need two because of smoother switching between color modes */
@keyframes fadeIn1 {
  from { opacity: 0; }
  to { opacity: 1; }
}
@keyframes fadeIn2 {
  from { opacity: 0; }
  to { opacity: 1; }
}

.drawer-toggle .bar {
  width: 90%;
  height: 2px;
  background-color: var(--color-primary);
}
.drawer-toggle {
  display: flex;
  justify-self: end;
  flex-direction: column;
  justify-content: space-around;
  height: 16px;
  width: 30px;
  cursor: pointer;
}
@media (max-width: 767px) {
  .app-links {
    display: none;
  }
}
@media (min-width: 768px) {
  .app-links {
    display: block;
  }
  .drawer-toggle {
    display: none;
  }
}
</style>
