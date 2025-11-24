<script setup lang="ts">
import { onMounted, ref } from "vue";
import TailwindShowcase from "./components/TailwindShowcase.vue";

const darkMode = ref(false);

function toggleTheme() {
  darkMode.value = !darkMode.value;
  document.documentElement.classList.toggle("dark", darkMode.value);
  document.documentElement.classList.toggle("light", !darkMode.value);
}

// Save theme preference
function saveTheme() {
  localStorage.setItem("theme", darkMode.value ? "dark" : "light");
}

onMounted(() => {
  const savedTheme = localStorage.getItem("theme");
  const prefersDark = window.matchMedia("(prefers-color-scheme: dark)").matches;

  darkMode.value = savedTheme ? savedTheme === "dark" : prefersDark;
  document.documentElement.classList.toggle("dark", darkMode.value);
  document.documentElement.classList.toggle("light", !darkMode.value);
});
</script>

<template>
  <div class="min-h-screen bg-white dark:bg-gray-900">
    <TailwindShowcase />

    <!-- Floating Theme Toggle Button -->
    <button
      @click="
        toggleTheme();
        saveTheme();
      "
      class="fixed top-4 right-4 z-50 p-3 rounded-lg bg-white dark:bg-gray-800 shadow-lg border border-gray-200 dark:border-gray-700 hover:bg-gray-100 dark:hover:bg-gray-700 text-gray-600 dark:text-gray-300 hover:text-blue-600 dark:hover:text-blue-400 transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
      title="Toggle theme"
    >
      <span v-if="darkMode" class="text-xl">🌙</span>
      <span v-else class="text-xl">☀️</span>
    </button>
  </div>
</template>
