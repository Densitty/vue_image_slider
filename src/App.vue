<template>
  <h2>Welcome to my Online Zoo Gallery</h2>
  <slider controls :indicators="true" :width="1000" :height="450"></slider>
</template>

<script>
import Slider from "./components/slider/Slider.vue";

export default {
  name: "App",
  components: {
    Slider,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
