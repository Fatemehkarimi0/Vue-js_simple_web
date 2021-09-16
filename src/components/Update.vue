<template>
    <div>
    <Header />
     <h1>Hello Update!</h1>
     <form class="add">
      <input type="text" name="name" placeholder="Enter Name" v-model="resturant.name" />
      <input type="text" name="contact" placeholder="Enter contact" v-model="resturant.contact" />
      <input type="text" name="address" placeholder="Enter Address" v-model="resturant.address" />
      <button v-on:click="update">Update New resturant</button>
     </form>
    </div>
  </template>

<script>
import Header from './Header.vue'
import axios from 'axios'

export default {
  name: 'Update',
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
  async  update () {
      const result=await axios.put("http://localhost:3000/resturant"+this.$route.params.id ,{
        name:this.resturant.name ,
        address:this.resturant.address ,
        contact:this.resturant.contact

      })
      if(result.status == 200){
        this.$router.push({ name: 'Home' })

      }
    }
  },
async  mounted () {
    const user = localStorage.getItem('user_info')
    if (!user) {
      this.$router.push({ name: 'signup' })
    }
    const result = await axios.get('http://localhost:3000/resturant/'+this.$route.params.id)
    this.resturant = this.result.data
  }
}
</script>
