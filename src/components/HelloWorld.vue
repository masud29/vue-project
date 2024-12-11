<template>
  <div class="hello">
    <Navbar></Navbar>
    <h1>Posts</h1><hr>
    <input type="text" v-model="searchterm" placeholder="search">
    <div v-for="post in filteredPosts" :key="post.id">
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
  
    </div>
  </div>
</template>

<script>
import Navbar from './Navbar.vue'
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data() {
    return {
      posts: [],
      searchterm: ''
    }
  },
  components: {
    Navbar
  },
  computed: {
    filteredPosts() {
      return this.posts.filter(post => post.title.toLowerCase().includes(this.searchterm.toLowerCase()))
    }
  },
  created(){
     axios.get('https://jsonplaceholder.typicode.com/posts/')
    .then(response => {
     this.posts = response.data
     })
    .catch(error => {
       console.log(error)
     })
  }
}
</script>

<style >
h1{
  color: red;
}

</style>
