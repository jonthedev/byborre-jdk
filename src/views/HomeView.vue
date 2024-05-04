<script setup>
import { ref } from 'vue'
import { useFirestore } from 'vuefire'
import { collection, query, getDocs, onSnapshot } from 'firebase/firestore'

const users = ref([])

const db = useFirestore()
const q = query(collection(db, 'users'))

const querySnapshot = await getDocs(q)
onSnapshot(q, (querySnapshot) => {
  users.value = []
  querySnapshot.forEach((doc) => {
    // doc.data() is never undefined for query doc snapshots
    console.log(doc.id, ' => ', doc.data())
    users.value.push(doc.data())
  })
})
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
