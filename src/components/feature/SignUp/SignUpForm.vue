<template>
  <div>
    <h2>Sign Up</h2>
    <form @submit.prevent="submitForm">
      <div>
        <label for="fullname">Full Name</label>
        <input type="text" id="fullname" v-model="fullname" required />
      </div>
      <div>
        <label for="email">Email</label>
        <input type="email" id="email" v-model="email" required />
      </div>
      <div>
        <label for="password">Password</label>
        <input type="password" id="password" v-model="password" required />
      </div>
      <button type="submit">Sign Up</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fullname: '',
      email: '',
      password: ''
    }
  },
  methods: {
    submitForm() {
      // Here you can handle form submission
      console.log('Full Name:', this.fullname)
      console.log('Email:', this.email)
      console.log('Password:', this.password)
    }
  }
}
</script>

<style>
/* Add your custom styles here */
</style>
