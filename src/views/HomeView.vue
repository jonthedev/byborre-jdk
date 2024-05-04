<script setup>
import { useFirestore, useCollection } from 'vuefire'
import { collection } from 'firebase/firestore'

const db = useFirestore()
const users = useCollection(collection(db, 'users'))
</script>

<template>
  <div class="background-color flex justify-center items-center h-full relative">
    <p class="text-4xl font-bold">
      Sign up successful! Welcome to BYBORRE Create<span class="trademark">&trade;</span>
    </p>
  </div>
</template>
