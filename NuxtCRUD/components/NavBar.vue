<template>
  <div class="nav">
    <nuxt-link to="/" class="brand">NUXT.js</nuxt-link>
    <nav>
      <nuxt-link class="link" to="/">Posts</nuxt-link>&nbsp;|
      <nuxt-link class="link" to="/create">Create</nuxt-link>
    </nav>
  </div>
</template>
    
<style scoped>
  .brand {
    font-family: 'Montserrat', sans-serif;
    font-weight: 700;
    font-size: 1.5em;
    color: #39b982;
    text-decoration: none;
  }
  .nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: aliceblue;
    padding: 5px 20px;
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