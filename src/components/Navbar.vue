<template>
  <div class="navbar">
      <nav class="main-nav">
          <router-link :to="{name: 'Home'}">Projects</router-link>
          <router-link :to="{name: 'Add'}">Add a new projects</router-link>
      </nav>
  </div>
</template>

<script>
export default {

}
</script>

<style>
.main-nav {
    text-align: center;
    margin: 40px auto;
}
.main-nav a {
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: #7f8c8d;
    font-size: 1.1em;
}
a.router-link-exact-active {
    border-bottom: 2px solid #2c3e50;
    padding-bottom: 4px;
}
</style>