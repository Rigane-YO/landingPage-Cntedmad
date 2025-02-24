<template>
  <button 
    class="theme-toggle" 
    @click="toggleTheme" 
    :title="isDark ? 'Passer en mode clair' : 'Passer en mode sombre'"
  >
    <i :class="isDark ? 'bi bi-sun' : 'bi bi-moon'"></i>
  </button>
  <router-view></router-view>
</template>

<script setup lang="ts">
import { ref, onMounted, watch } from 'vue'

const isDark = ref(false)

const toggleTheme = () => {
  isDark.value = !isDark.value
  document.documentElement.setAttribute('data-theme', isDark.value ? 'dark' : 'light')
}

onMounted(() => {
  // Check system preference
  const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches
  isDark.value = prefersDark
  document.documentElement.setAttribute('data-theme', prefersDark ? 'dark' : 'light')
})
</script>

<style>
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css");

#app {
  max-width: 100%;
  margin: 0;
  padding: 0;
  text-align: left;
}
</style>