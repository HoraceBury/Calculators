<template>
  <div class="hello">
    <h2>Stock Profit</h2>
    <ul>
      <li>
        <p>( Close / Open ) x ( Leverage x Investment ) - ( Leverage x Investment ) = $profit</p>
        <p>( <input v-model="close" placeholder="close" size=4> / <input v-model="open" placeholder="open" size=4> ) x ( <input v-model="leverage" placeholder="leverage" size=4> x $<input v-model="investment" placeholder="investment" size=4> ) - ( <input v-model="leverage" placeholder="leverage" size=4> x $<input v-model="investment" placeholder="investment" size=4> ) = ${{profit}}</p>
        <p>( {{close}} / {{open}} ) x ( {{leverage}} x ${{investment}} ) - ( {{leverage}} x ${{investment}} ) = ${{profit}}</p>
      </li>
    </ul>
  </div>
  <div>
    <h2>Percentage Increase</h2>
    <ul>
      <li>
        <p>( ( Close - Open ) / Open ) * 100 = %increase</p>
        <p>( ( <input v-model="close" placeholder="close" size=4> - <input v-model="open" placeholder="open" size=4> ) / <input v-model="open" placeholder="open" size=4> ) * 100 = {{percentage}}%</p>
        <p>( ( {{close}} - {{open}} ) / {{open}} ) * 100 = {{percentage}}%</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      'close': 4486.98,
      'open': 4377.46,
      'leverage': 20,
      'investment': 200
    }
  },
  computed: {
    profit () {
      return ((this.close / this.open) * (this.leverage * this.investment) - (this.leverage * this.investment)).toFixed(2)
    },
    percentage () {
      return (((this.close-this.open)/this.open)*100).toFixed(2)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
