<template>
  <div id="app">
    <header>
    </header>
    <main>
      <Calculator />
    </main>
    <footer>
      <p>&copy; 2023 Mokammel Tanvir. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue';

export default {
  name: 'App',
  components: {
    Calculator,
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
}

header,
footer {
  /* Add styling for header and footer if needed */
}

main {
  padding: 20px;
}
</style>
