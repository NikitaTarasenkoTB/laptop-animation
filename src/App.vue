<template>
  <div id="app">
    <Laptop />
  </div>
</template>

<script>
import Laptop from "./components/Laptop.vue";

export default {
  name: "App",
  components: {
    Laptop
  }
};
</script>

<style>
body {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  background: coral;
}
</style>
