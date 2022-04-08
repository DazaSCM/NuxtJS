<template>
  <div class="container pd-40">
    <h3 class="text-center m-3">Post Lists</h3>
    <div class="d-flex justify-content-center mb-4">
      <input type="text" class="form-control w-400" @keyup="isClear" placeholder="Search by User ID" v-model="user_id">
      <button class="btn btn-primary" @click="search">Search</button>
    </div>
    
    <table class="table table-hover">
      <thead>
        <tr>
          <td>UserID</td>
          <td>ID</td>
          <td class="text-center">Title</td>
          <td colspan="2" class="text-center">Actions</td>
        </tr>
      </thead>

      <tbody>
        <tr v-for="post in posts" :key="post.id">
          <td>{{ post.userId}}</td>
          <td>{{ post.id }}</td>
          <td>{{ post.title }}</td>
          <td><nuxt-link :to="{ path: 'details', query: { id: post.id }}" class="btn btn-info">Details</nuxt-link></td>
          <td><button @click="deletePost(post.id)" class="btn btn-danger">Delete</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      posts: [],
      user_id: ''
    }
  },
  created:function () {
    this.getAll();
  },
  methods: {
    async getAll() {
      this.posts = await fetch(
        'https://jsonplaceholder.typicode.com/posts'
      ).then((res) => res.json())
    },
    async search(){
      this.posts = await fetch(
        'https://jsonplaceholder.typicode.com/posts?userId='+this.user_id
      ).then((res) => res.json())
    },
    isClear() {
      if(!this.user_id) {
        this.getAll();
      }
    },
    deletePost(id) {
      fetch('https://jsonplaceholder.typicode.com/posts/'+id, {
        method: 'DELETE',
      }).then(() =>
        console.log("post deleted"));
    }
  }
}
</script>

<style>
  .pd-40 {
    padding: 0 40px;
  }
  .w-400 {
    width: 400px;
    margin-right: 30px;
  }
</style>