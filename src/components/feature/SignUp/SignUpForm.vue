<template>
  <div class="signup-form">
    <h2 class="signup-form__title">
      Sign up for Create <span class="signup-form__trademark">&trade;</span>
    </h2>
    <form class="signup-form__form" @submit.prevent="submitForm">
      <div class="signup-form__field">
        <input
          type="email"
          id="email"
          v-model="newUser.email"
          class="signup-form__input"
          required
          placeholder="Email Address*"
        />
      </div>
      <div class="signup-form__field">
        <input
          type="text"
          id="fullName"
          v-model="newUser.fullName"
          class="signup-form__input"
          required
          placeholder="Full Name*"
        />
      </div>
      <div class="signup-form__field">
        <input
          type="password"
          id="password"
          v-model="newUser.password"
          class="signup-form__input"
          required
          placeholder="Create password"
          minlength="8"
        />
        <span class="signup-form__hint">minimum of 8 characters</span>
      </div>
      <button type="submit" class="signup-form__button" @click.prevent="signUpNewUser">
        <span>Sign Up</span> <span class="signup-form__button--arrow">&#8594;</span>
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { collection, addDoc } from 'firebase/firestore'
import { useFirestore } from 'vuefire'

const db = useFirestore()
const router = useRouter()

const newUser = ref({
  fullName: '',
  email: '',
  password: ''
})

async function signUpNewUser() {
  if (newUser.value.password.length < 8) {
    return
  }
  // Add a new document with a generated id.
  const newDoc = await addDoc(collection(db, 'users'), {
    ...newUser.value
  })

  if (newDoc.id) {
    router.push('/')
  }
}
</script>
<style scoped>
.signup-form {
  @apply flex flex-col h-[37.5rem] w-[28.125rem] bg-white rounded-2xl p-9;
}

.signup-form__title {
  @apply text-4xl font-light mb-4;
}

.signup-form__form {
  @apply flex flex-col flex-1;
}

.signup-form__field {
  @apply w-full mb-4;
}

.signup-form__input {
  @apply w-full p-2.5 rounded-lg border-[#adabab] border-solid border-[1px];
}

.signup-form__field:last-of-type {
  @apply grow;
}

.signup-form__hint {
  @apply block text-[#adabab] mt-2;
}

.signup-form__button {
  @apply text-white flex items-center justify-center p-4 rounded-[50px] bg-black;
}

.signup-form__button--arrow {
  @apply ml-2;
}
</style>
