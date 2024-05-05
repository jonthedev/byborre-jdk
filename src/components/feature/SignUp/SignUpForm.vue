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
  height: 600px;
  width: 450px;
  background: #fff;
  border-radius: 20px;
  padding: 35px;

  display: flex;
  flex-direction: column;
}

.signup-form__title {
  font-size: 35px;
  font-weight: 300;
  margin-bottom: 0.5rem;
}

.signup-form__form {
  display: flex;
  flex-direction: column;
  flex: 1;
}

.signup-form__field {
  width: 100%;
  margin-bottom: 1rem;
}

.signup-form__input {
  border: #adabab solid 1px;
  width: 100%;
  padding: 10px;
  border-radius: 10px;
}

.signup-form__field:last-of-type {
  flex-grow: 1;
}

.signup-form__hint {
  margin-top: 0.5rem;
  display: block;
  color: #adabab;
}

.signup-form__button {
  background: #000;
  color: #fff;
  border-radius: 50px;
  padding: 1rem;

  display: flex;
  align-items: center;
  justify-content: center;
}

.signup-form__button--arrow {
  margin-left: 8px;
}
</style>
