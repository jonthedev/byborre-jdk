<script setup>
import { useFirestore, useCollection } from 'vuefire'
import { collection } from 'firebase/firestore'

const db = useFirestore()
const users = useCollection(collection(db, 'users'))
</script>

<template>
  <nav
    className="sticky top-0 z-10 h-16 shadow-sm shadow-slate-950"
    id="navbar"
    data-testid="navbar"
  >
    BYBORRE
  </nav>
  <div class="background-color flex justify-center items-center h-full">
    <p class="text-4xl font-bold">
      Sign up successfull! Welcome to BYBORRE Create<span class="trademark">&trade;</span>
    </p>
  </div>
</template>
