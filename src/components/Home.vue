<template>
    <div>
    <Header />
     <h1>Hello {{name}}</h1>
     <table border="1 ">
       <tr v-for="item in resturant" :key="item.id" >
         <td>{{item.id}}</td>
         <td>{{item.name}}</td>
         <td>{{item.contact}}</td>
         <td>{{item.address}}</td>
         <td><router-link :to="'/update'+item.id">Update</router-link>
        <button v-on:click="delete(item.id)">Delete</button>
      </td>
       </tr>
     </table>
    </div>
  </template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
  name: 'Home',
    data () {
    return {
     name: '',
     resturant: []
    }
  },
  components: {
    Header
  },
  methods: {
  async delete(id){
      let result = await axios.delete('http://localhost:3000/resturant'+id)
      if(result.status == 200){
        this.loadData()

      }
    },
    async  loadData() {
    const user = localStorage.getItem('user_info')
    this.name = JSON.parse(user).name;
    if (!user) {
      this.$router.push({ name: 'signup' })
    }
    let result = await axios.get('http://localhost:3000/resturant')
    this.resturant=result.data;
    }
  },
  async mounted () {
    this.loadData()
  }
}
</script>
