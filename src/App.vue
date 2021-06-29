<template>
  <div id="app">
    <PizzaForm />
  </div>
</template>

<script>
import PizzaForm from './components/PizzaForm.vue'

export default {
  name: 'App',
  components: {
    PizzaForm
  }
}
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
