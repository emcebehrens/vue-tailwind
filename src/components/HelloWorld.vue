<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const count = ref(0)
</script>

<template>
  <h1 class="mb-6 text-primary dark:text-primary-dark">{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++" class="text-primary dark:text-primary-dark">
      count is {{ count }}
    </button>
    <p class="text-primary dark:text-primary-dark">
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p class="text-primary dark:text-primary-dark">
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p class="text-primary dark:text-primary-dark">
    Learn more about IDE Support for Vue in the
    <a
      href="https://vuejs.org/guide/scaling-up/tooling.html#ide-support"
      target="_blank"
      >Vue Docs Scaling up Guide</a
    >.
  </p>
</template>

<style scoped>

</style>
