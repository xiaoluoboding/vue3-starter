<template>
  <header>
    <img
      alt="Vue logo"
      class="block mx-auto mt-0 mb-8 lg:mr-8"
      src="@/assets/logo.svg"
      width="125"
      height="125"
    />
    <div class="wrapper" lg="flex place-items-center flex-wrap">
      <HelloWorld :msg="$t('hello', { name: 'A better Vue 3 Starter' })" />
      <nav
        class="w-full text-xs text-center mt-8"
        lg="text-left text-base py-4 px-0 mt-4 -ml-4"
      >
        <RouterLink to="/">{{ $t('menu.home') }}</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
      <div class="w-full text-center mt-8 space-x-4" lg="text-left">
        <button
          border="~ [var(--color-border)]"
          class="p-2 rounded-md bg-transparent"
          @click="(e) => toggleDark()"
        >
          <carbon:moon class="w-6 h-6" v-if="isDark" />
          <carbon:sun class="w-6 h-6" v-else />
        </button>
        <button
          border="~ [var(--color-border)]"
          class="p-2 rounded-md bg-transparent"
          @click="toggleLocales"
        >
          <carbon:language class="w-6 h-6" />
        </button>
        <button
          border="~ [var(--color-border)]"
          class="p-2 rounded-md bg-transparent"
          @click="gotoGitHub"
        >
          <carbon:logo-github class="w-6 h-6" />
        </button>
      </div>
    </div>
  </header>

  <RouterView />
</template>

<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { useI18n } from 'vue-i18n'

import HelloWorld from '@/components/HelloWorld.vue'
import { isDark, toggleDark } from '@/composables/useDarkmode'
import { availableLocales, loadLanguageAsync } from '@/plugins/i18n'

const { locale } = useI18n()

const gotoGitHub = () => {
  window.open('https://github.com/xiaoluoboding/vue3-starter', '_blank')
}

async function toggleLocales() {
  // change to some real logic
  const locales = availableLocales
  const newLocale =
    locales[(locales.indexOf(locale.value) + 1) % locales.length]
  await loadLanguageAsync(newLocale)
  locale.value = newLocale
}
</script>

<style>
@import '@/assets/base.css';

#app {
  @apply max-w-screen-xl mx-auto my-0 p-8 font-normal;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1) !important;
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }
}
</style>
