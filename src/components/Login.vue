<template>
  <img class="logo" src="../assets/logo.png" />
  <h1>Login</h1>
  <div class="register">
    <input type="text" v-model="email" placeholder=" Enter Email" />
    <input type="text" v-model="password" placeholder=" Enter Password" />
    <button v-on:click="login">Login</button>
    <p>
    <router-link to='/signup'>Signup</router-link>
    </p>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'Login',
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    async login () {
      const result = await axios.get(
      `http://localhost:3000/users?email=${this.email}&password=${this.password}`
      )
      if (result.status === 200) {
        localStorage.setItem('user_info', result.data[0])
        this.$router.push({ name: 'Home' })
      }
      console.log(result)
    }
  },
  mounted () {
    const user = localStorage.getItem('user_info')
    if (user) {
      this.$router.push({ name: 'Home' })
    }
  }
}
</script>
