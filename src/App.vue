<template>
  <Calculator />
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "App",
  components: {
    Calculator,
  },
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  text-align: center;
  background-image: url("calculate.jpg");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
</style>
