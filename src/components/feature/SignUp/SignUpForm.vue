<template>
  <div>
    <h2>Sign up for Create <span class="trademark">&trade;</span></h2>
    <form @submit.prevent="submitForm">
      <div>
        <label for="fullName">Full Name</label>
        <input type="text" id="fullName" v-model="newUser.fullName" required />
      </div>
      <div>
        <label for="email">Email</label>
        <input type="email" id="email" v-model="newUser.email" required />
      </div>
      <div>
        <label for="password">Password</label>
        <input type="password" id="password" v-model="newUser.password" required />
      </div>
      <button type="submit" @click.prevent="signUpNewUser">Sign Up</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { collection, addDoc } from 'firebase/firestore'
import { useFirestore } from 'vuefire'

const db = useFirestore()

const newUser = ref({
  fullName: '',
  email: '',
  password: ''
})

async function signUpNewUser() {
  // Add a new document with a generated id.
  const newDoc = await addDoc(collection(db, 'users'), {
    ...newUser.value
  })

  console.log(newDoc)
}
</script>