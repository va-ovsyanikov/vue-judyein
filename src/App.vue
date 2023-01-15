<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" width="25%">
    <example1/>
    <example2/>
  </div>
</template>

<script>
import Example1 from "./components/Example1";
import Example2 from "./components/Example2";

export default {
  name: "App",
  components: {
    Example1,
    Example2
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
