<template>
  <div id="app">
    <div class="laptopContainer" :key="speed">
      <Laptop @setSpeed="setSpeed" :speed="speed"/>
    </div>
  </div>
</template>

<script>
import Laptop from "./components/Laptop.vue";

export default {
  name: "App",
  components: {
    Laptop
  },
  data() {
    return {
      speed: 0.1
    }
  },
  methods: {
    setSpeed(value) {
      this.speed += value;
      console.log(this.speed, 'speed');
    }
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
