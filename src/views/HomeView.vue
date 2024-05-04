<script setup>
import { useFirestore, useCollection } from 'vuefire'
import { collection } from 'firebase/firestore'

const db = useFirestore()

const users = useCollection(collection(db, 'users'))
</script>

<template>
  <div>
    <h2>List of Users</h2>
    <ul v-if="users.length > 0">
      <li v-for="user in users" :key="user.id">
        <div>{{ user.fullName }}</div>
        <div>{{ user.email }}</div>
      </li>
    </ul>
    <div v-else>No users found.</div>
  </div>
</template>
