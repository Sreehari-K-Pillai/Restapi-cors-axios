<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
     <div class="card-body">
  <form @submit="formSubmit">
   <div>
  <strong >Name:</strong>
  <input type="text"  v-model="name">
  </div>
  <div>
   <strong>Position:</strong>
    <textarea  v-model="position"></textarea>
     </div>
     <button>Add User</button>
    </form>
    <button @click="getUser">Get User</button>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from "axios";
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data () {
    return {
      name: '',
      position: '',
    }
  },
  methods: {
    getUser() {
      axios.get('http://localhost:3030/data/getuser').then(function(response) {
        // if(response.ok) {
        //   return response.json()
        // }
        // }).then(function(data) {
          console.log(response.data)
      }) 
    },
      formSubmit(e) {
          e.preventDefault();
          axios.post('http://localhost:3030/data/adduser', {
                user: this.name,
                password: this.position
          })
          .then(response => (console.log(response.data)))
          .catch(error => console.log(error))
          .finally(() => this.loading = false)
      }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
