<template>
<header>
<h1>Sexy Crafted Beers</h1>
</header>
<ul>
  <div id="container">
        <label for="name">Search for name:</label>
        <input v-model="beerFilter" id="name">
        <label for="food">Search for food pairing:</label>
        <input v-model="beerFilter" id="food">
        <label for="name">Search for name:</label>
        <input v-model="beerFilter" id="name">
  </div>
</ul>
<ul>
  <div id="container">

    <OneBeer
    v-for="beer in filterByInput"
    :key="beer.id"
    :id="beer.id"
    :name="beer.name"
    :image-url="beer.image_url"
    ></OneBeer>
  </div>
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
  background: #2193b0;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to bottom, #2193b0, #6dd5ed);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to bottom, #2193b0, #6dd5ed); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

}
h1 {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: #FBD786;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}
label {

}
input {
  max-width: 8em;
}
#container {
  width: 90%;
  margin: 0 auto;
  border: 5px solid #22c1c3;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  background: #2193b0;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to bottom, #6dd5ed, #2193b0);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to bottom, #6dd5ed, #2193b0); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

}
#container li {
  width: 400px;
  height:500px;
  color: #ffa260;
  border: 2px solid;
  font-size: 0,7em;
  transition: color 0.5s, border-color 0.5s, box-shadow 0.5s, transform 0.5s;
}
#container li:hover {
  border-color: #f1ff5c;
  color: white;
  box-shadow: 0 0,5em 0.5em -0.4em #f1ff5c;
  transform: translateY(-0.25em);
  cursor: pointer;
}
img {
  max-width: 5rem;
  max-height: 8em;
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
  background: #2193b0;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to bottom, #2193b0, #6dd5ed);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to bottom, #2193b0, #6dd5ed); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

}
</style>
