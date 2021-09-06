<template>
  <div class="hello">
    <h2>Stock Profit</h2>
    <ul>
      <li>
        <p>( Close / Open ) x ( Leverage x Investment ) - ( Leverage x Investment ) = $</p>
        <p>( <input v-model="sp_close" placeholder="close" size=4> / <input v-model="sp_open" placeholder="open" size=4> ) x ( <input v-model="sp_leverage" placeholder="leverage" size=4> x $<input v-model="sp_investment" placeholder="investment" size=4> ) - ( <input v-model="sp_leverage" placeholder="leverage" size=4> x $<input v-model="sp_investment" placeholder="investment" size=4> ) = ${{sp_profit}}</p>
        <p>( {{sp_close}} / {{sp_open}} ) x ( {{sp_leverage}} x ${{sp_investment}} ) - ( {{sp_leverage}} x ${{sp_investment}} ) = ${{sp_profit}}</p>
      </li>
    </ul>
  </div>
  <div>
    <h2>Percentage Increase</h2>
    <ul>
      <li>
        <p>( ( Close - Open ) / Open ) * 100 = %</p>
        <p>( ( <input v-model="pc_close" placeholder="close" size=4> - <input v-model="pc_open" placeholder="open" size=4> ) / <input v-model="pc_open" placeholder="pc_open" size=4> ) * 100 = {{pc_percentage}}%</p>
        <p>( ( {{pc_close}} - {{pc_open}} ) / {{pc_open}} ) * 100 = {{pc_percentage}}%</p>
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
      'sp_close': 4486.98,
      'sp_open': 4377.46,
      'sp_leverage': 20,
      'sp_investment': 200,
      'pc_open': 4377.46,
      'pc_close': 4486.98
    }
  },
  computed: {
    sp_profit () {
      return ((this.sp_close / this.sp_open) * (this.sp_leverage * this.sp_investment) - (this.sp_leverage * this.sp_investment)).toFixed(2)
    },
    pc_percentage () {
      return (((this.pc_close-this.pc_open)/this.pc_open)*100).toFixed(2)
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
