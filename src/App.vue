<template>
  <NavBar />
  <router-view />
</template>

<script>
import NavBar from "../src/components/NavBar.vue";
export default {
  components: { NavBar },
};
</script>
<style>
body {
  background-color: #f2f0f0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 60rem;
  margin: 0 auto;
  color: #2c3e50;
}
</style>
