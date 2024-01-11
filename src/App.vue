<template>
  <!-- <Calculator /> -->
  <NewCalculator></NewCalculator>
</template>

<script>
// import Calculator from "./components/Calculator.vue";
import NewCalculator from "./components/NewCalculator.vue";

export default {
  name: "App",
  components: {
    // Calculator,
    NewCalculator,
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
