<template>
  <img class="logo" src="../assets/logo.png" />
  <h1>SignUp</h1>
  <div class="register">
    <input type="text" v-model="name" placeholder=" Enter Name" />
    <input type="text" v-model="email" placeholder=" Enter Email" />
    <input type="text" v-model="password" placeholder=" Enter Password" />
    <button v-on:click="signup">SignUp</button>
    <p>
    <router-link to='/login'>Login</router-link>
    </p>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'SignUp',
  data () {
    return {
      name: '',
      email: '',
      password: ''
    }
  },
  methods: {
    async  signup () {
      const result = await axios.post('http://localhost:3000/users', {
        email: this.email,
        password: this.password,
        name: this.name
      })
      // ({ //   method: "POST",
      //   url: "http://localhost:3000/users",
      //   data: {
      //     email: this.email,
      //     password: this.password,
      //     name: this.name,
      //   },
      //   headers: {
      //     "Access-Control-Allow-Origin": "*",
      //     "Content-type": "application/json",
      //   },
      // });
      // Some if here
      // console.warn(result);
      // console.log("kkkkk");
      if (result.status === 201) {
        localStorage.setItem('user_info', result)
        this.$router.push({ name: 'Home' })
      }
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

<style scoped>
.logo {
  width: 100px;
}
.register input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin: 0 auto 30px auto;
  border: 1px solid skyblue;
}
.register button {
  width: 320px;
  height: 40px;
  border: 1px solid skyblue;
  background: skyblue;
  color: #fff;
  cursor: pointer;
}
</style>
