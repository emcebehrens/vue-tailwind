<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import { onMounted, ref } from 'vue'

const darkMode = ref(false)

function toggleTheme() {
  darkMode.value = !darkMode.value
  document.documentElement.classList.toggle('dark', darkMode.value)
  document.documentElement.classList.toggle('light', !darkMode.value)
}

// Save theme preference
function saveTheme() {
  localStorage.setItem('theme', darkMode.value ? 'dark' : 'light')
}

onMounted(() => {
  // Check for saved theme or default to system preference
  const savedTheme = localStorage.getItem('theme')
  const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches
  
  darkMode.value = savedTheme ? savedTheme === 'dark' : prefersDark
  document.documentElement.classList.toggle('dark', darkMode.value)
  document.documentElement.classList.toggle('light', !darkMode.value)
})
</script>

<template>
  <div class="min-h-screen bg-background dark:bg-background-dark">
    <header class="sticky top-0 bg-white/80 dark:bg-gray-800/80 backdrop-blur-md border-b border-gray-200 dark:border-gray-700 z-10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center h-16">
          <h1 class="text-xl font-bold text-blue-600">Geo UI</h1>
          <button 
            @click="toggleTheme(); saveTheme()"
            class="p-2 rounded-lg bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-gray-600 dark:text-gray-300 hover:text-blue-600 dark:hover:text-blue-400 transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
          >
            <span v-if="darkMode">🌙</span>
            <span v-else>☀️</span>
          </button>
        </div>
      </div>
    </header>
    
    <HelloWorld msg="Vite + Vue" />
  </div>
</template>

<style scoped>

</style>
