<template>
  <nav class="main-nav">
    <router-link :to="{ name: 'Home' }">Home</router-link>
    <router-link :to="{ name: 'AddProject' }">Add a New Project</router-link>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
};
</script>

<style>
.main-nav {
  width: 100%;
  text-align: center;
  margin: 30px 0;
}

.main-nav a {
  padding: 10px;
  text-decoration: none;
  /* text-transform: uppercase; */
  color: #bbb;
  font-size: 18px;
}

.main-nav a:not(:first-child) {
  margin-left: 16px;
}

.main-nav a.router-link-exact-active {
  border-bottom: 2px solid #00ce89;
}
</style>
