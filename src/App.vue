<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import { onMounted } from 'vue'

onMounted(() => {
  // Check for saved theme or default to system preference
  // const savedTheme = localStorage.getItem('theme')
  // const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches
  
  // darkMode.value = savedTheme ? savedTheme === 'dark' : prefersDark
  // document.documentElement.classList.toggle('dark', darkMode.value)
  // document.documentElement.classList.toggle('light', !darkMode.value)

  // Set dark theme by default
  document.documentElement.classList.toggle('dark', false)
})
</script>

<template>
  <div class="min-h-screen bg-background dark:bg-background-dark">
    <HelloWorld msg="Vite + Vue" />
  </div>
</template>

<style scoped>

</style>
