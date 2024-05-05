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
      <button type="submit" class="signup-form__button" @click.prevent="createUser">
        <span>Sign Up</span> <span class="signup-form__button--arrow">&#8594;</span>
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { useFirebaseAuth } from 'vuefire'
import { createUserWithEmailAndPassword } from 'firebase/auth'
import { updateProfile } from 'firebase/auth'

const router = useRouter()
const auth = useFirebaseAuth()

const newUser = ref({
  fullName: '',
  email: '',
  password: ''
})

async function createUser() {
  try {
    const userCredential = await createUserWithEmailAndPassword(
      auth,
      newUser.value.email,
      newUser.value.password
    )
    const user = userCredential.user

    await updateProfile(user, {
      displayName: newUser.value.fullName
    })

    newUser.value.fullName = ''
    newUser.value.email = ''
    newUser.value.password = ''

    router.push('/')
  } catch (error) {
    console.error('Error signing up:', error.message)
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
