<template>
  <a href="https://github.com/HoraceBury/Calculators">Source</a>
  <StockProfit/>
</template>

<script>
import StockProfit from './components/StockProfit.vue'

export default {
  name: 'App',
  components: {
    StockProfit
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
