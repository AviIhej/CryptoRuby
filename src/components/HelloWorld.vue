<template>
  <div class="hello">
    <div id="crypto-container" v-for="(value, key) in cryptos">
      <span class="left">{{ key }}</span>
      <span class="right">${{ value.USD }}</span>
    </div>
  </div>
</template>

<script>

// Get call to cryptocompare
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data: () => ({
    cryptos: [],
    errors: []
  }),

// Anything inside the created function will be run when the component loads
// Url of the API endpoint
// We want BTC=bitcoin, ETH=etherium, IOT=iota & USD amount of each one
  created () {
    axios.get('https://min-api.cryptocompare.com/data/pricemulti?fsyms=BTC,ETH,IOT&tsyms=USD')
    .then(response => {
      this.cryptos = response.data
      console.log(response)
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
body{
  background: lightgray;
}

div#crypto-container{
  background: white;
  width: 70%;
  margin: 0 auto 4px auto;
  padding: 1em;
  box-shadow: 1px 1px 0 lightgrey;
  
}

span.left{
  font-weight: bold;
}

span.right{
  float: right;
}
</style>
