<template>
  <NewCalculator></NewCalculator>
  <CalculatePoly></CalculatePoly>
</template>

<script>
import NewCalculator from "./components/NewCalculator.vue";
import CalculatePoly from "./components/CalculatePoly.vue";

export default {
  name: "App",
  components: {
    NewCalculator,
    CalculatePoly,
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
}
</style>
