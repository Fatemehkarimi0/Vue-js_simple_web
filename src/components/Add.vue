<template>
    <div>
    <Header />
     <h1>Hello EveryBody to Add!</h1>
     <form class="add">
      <input type="text" name="name" placeholder="Enter Name" v-model="resturant.name" />
      <input type="text" name="contact" placeholder="Enter contact" v-model="resturant.contact" />
      <input type="text" name="address" placeholder="Enter Address" v-model="resturant.address" />
      <button v-on:click="add">Add New resturant</button>
     </form>
    </div>
  </template>

<script>
import Header from './Header.vue'
import axios from 'axios'

export default {
  name: 'Add',
  components: {
    Header
  },
  data () {
    return {
      Resturant :{
        name: '',
        contact: '',
        address: ''
      }
    }
  },
  methods: {
  async  add () {
      const result=await axios.post("http://localhost:3000/resturant",{
        name:this.resturant.name ,
        address:this.resturant.address ,
        contact:this.resturant.contact

      })
      if(result.status == 201){
        this.$router.push({ name: 'Home' })

      }
    }
  },
  mounted () {
    const user = localStorage.getItem('user_info')
    if (!user) {
      this.$router.push({ name: 'signup' })
    }
  }
}
</script>
