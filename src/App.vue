<script>
import Navbar from './components/Navbar.vue';

export default {
  components: { Navbar }
}
</script>

<template>
  <nav>
    <Navbar></Navbar>
  </nav>
  <router-view />
</template>

<style>
body {
  background: #f2f2f2;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: #555;
}

/* nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
} */
</style>
