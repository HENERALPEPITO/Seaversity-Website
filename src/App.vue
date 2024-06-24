<script setup>
import { ref, computed } from 'vue'
import Home from './Home.vue'
import About from './About.vue'
import NotFound from './NotFound.vue'
import blog from './blog.vue'

const routes = {
  '/': Home,
  '/about': About,
  '/blog': blog
}

const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || NotFound
})
</script>

<template>
  <div class="navbar">
    <img src="./logo/logo.jpeg" alt="Logo" class="logo">
    <a href="#/">Home</a> |
    <a href="#/about">About</a> |
    <a href="#/non-existent-path">Broken Link</a> |
    <a href="#/blog">Blog</a>
  </div>
  <component :is="currentView" />
</template>

<style>
.navbar {
  display: flex;
  align-items: center;
}

.logo {
  margin-right: 10px;
  height: 40px; 
}
</style>
