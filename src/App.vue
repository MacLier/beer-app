<template>
<header>
<h1>Sexy Crafted Beers</h1>
</header>
<ul>
  <OneBeer
  v-for="beer in beers"
  :key="beer.id"
  :id="beer.id"
  :name="beer.name"
  :image-url="beer.image_url"
  ></OneBeer>
</ul>
<p>{{info}}</p>
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
      beers: []
    }
  },
  mounted () {
    axios
      .get('https://api.punkapi.com/v2/beers')
      .then((response) => (this.beers = response.data))
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
