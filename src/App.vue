<script setup>
import { RouterView, useRoute } from 'vue-router'
import NavBar from './components/NavBar.vue'

const route = useRoute()
</script>

<template>
  <NavBar />
  <Suspense>
    <RouterView :key="route.fullPath" />
    <template #fallback> Loading.... </template>
  </Suspense>
</template>

<style scoped></style>
