<template>
<p>{{info}}</p>
  <OneBeer></OneBeer>
</template>

<script>
import OneBeer from './components/OneBeer.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    OneBeer
  },
  data () {
    return {
      info: null
    }
  },
  mounted () {
    axios
      .get('https://api.punkapi.com/v2/beers')
      .then((response) => (this.info = response.data))
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
