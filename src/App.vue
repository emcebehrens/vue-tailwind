<script setup lang="ts">
import HelloWorld from "./components/HelloWorld.vue";
import { onMounted } from "vue";

onMounted(() => {
  // Set dark theme by default
  document.documentElement.classList.toggle("dark", false);
});
</script>

<template>
  <div class="min-h-screen bg-background dark:bg-background-dark">
    <HelloWorld msg="Vite + Vue" />
  </div>
</template>

<style scoped></style>
