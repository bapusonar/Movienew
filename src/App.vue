<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Home />
  </div>
</template>

<script>
import Home from "./components/Home.vue";
export default {
  name: "app",
  components: { Home },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
}

body,
html {
  margin: 0px;
  padding: 0px;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif !important;
}
</style>
