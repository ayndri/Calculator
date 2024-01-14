<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <CalculatorApp msg="Calculator"/>
</template>

<script>
// import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'

// Import Bootstrap and BootstrapVue CSS files (order is important)
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
import CalculatorApp from './components/CalculatorApp.vue';

export default {
  name: 'App',
  components: {
    CalculatorApp
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
