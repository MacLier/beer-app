<template>
<header>
<h1>Sexy Crafted Beers</h1>
</header>
<input v-model="beerFilter">
<ul>

  <OneBeer
  v-for="beer in filterByInput"
  :key="beer.id"
  :id="beer.id"
  :name="beer.name"
  :image-url="beer.image_url"
  ></OneBeer>
</ul>
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
      beerFilter: '',
      beers: null
    }
  },
  mounted () {
    axios
      .get('https://api.punkapi.com/v2/beers')
      .then((response) => (this.beers = response.data))
  },
  watch: {
  },
  computed: {
    filterByInput () {
      if (this.beers) {
        return this.beers.filter(filteredBeer => {
          return filteredBeer.name.toLowerCase().includes(this.beerFilter)
        })
      }
      return []
    }
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
body {
  margin: 0;
  padding: 0;
}
header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: #009900;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}
ul{
  list-style: none;
}
li {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 1rem auto;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}
</style>
