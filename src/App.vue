<script setup>
import { RouterView, useRoute } from 'vue-router'

const route = useRoute()
</script>

<template>
  <Suspense>
    <RouterView :key="route.fullPath" />
    <template #fallback> Loading.... </template>
  </Suspense>
</template>

<style scoped></style>
