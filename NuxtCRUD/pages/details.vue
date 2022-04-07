<template>
  <div class="container w-800 m-top">
    <h3 class="text-center mb-3">Post Details</h3>
    <div class="row">
      <ul class="col-left">
        <li>User ID : </li>
        <li>Post ID : </li>
        <li>Title : </li>
        <br>
        <li>Body : </li>
      </ul>
      <ul class="col-right">
        <li>{{post.userId}}</li>
        <li>{{post.id}}</li>
        <li>{{post.title}}</li>
        <li>{{post.body}}</li>
      </ul>
    </div>
    <div class="d-flex justify-content-between">
      <nuxt-link class="link" :to="{ path: '/'}">Go Back?</nuxt-link>
      <nuxt-link class="link" :to="{ path: 'edit', query: {id: post.id}}">Edit?</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      post: []
    }
  },
  async fetch () {
    this.post = await fetch(
      'https://jsonplaceholder.typicode.com/posts/'+this.$nuxt._route.query.id
    ).then(res => res.json())
  }
}
</script>

<style>
  .w-800 {
    max-width: 800px;
  }
  .m-top {
    margin: 80px auto auto auto;
    background: antiquewhite;
    padding: 30px;
  }
  ul {
    list-style-type: none;
    line-height: 2;
  }
  .col-left {
    text-align: right;
    width: 48%;
  }
  .col-right {
    width: 52%;
    text-align: left;
  }
  .link {
    display: inline-block;
    font-size: 16px;
    text-decoration: none;
    font-weight: bold;
  }
  
  .link:hover {
    color: orangered;
  }
</style>