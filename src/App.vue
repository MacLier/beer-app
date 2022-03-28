<template>
  <header>
    <h1>Sexy Crafted Beers</h1>
  </header>
  <div>
    <div id="container">
        <div class="inputs">
          <label for="name">&nbsp;Filter in names&nbsp;</label>
          <input v-model="nameFilter" id="name">
        </div>
        <div class="inputs">
          <label for="food">&nbsp;Filter in food pairing&nbsp;</label>
          <input v-model="foodPairingFilter" id="food">
        </div>
        <div class="inputs">
          <label for="description">&nbsp;Filter in desription&nbsp;</label>
          <input v-model="descriptionFilter" id="description">
        </div>
    </div>
  </div>
  <div>
    <div id="container">

      <OneBeer
      v-for="beer in filterByInput"
      :key="beer.id"
      :id="beer.id"
      :name="beer.name"
      :image-url="beer.image_url"
      :description="beer.description"
      :tagline="beer.tagline"
      :food-pairing="beer.food_pairing"
      ></OneBeer>
    </div>
  </div>

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
      nameFilter: '',
      descriptionFilter: '',
      foodPairingFilter: '',
      beers: []
    }
  },
  mounted () {
    axios
      .get('https://api.punkapi.com/v2/beers')
      .then((response) => {
        this.beers = response.data.sort((a, b) => {
          return a.name > b.name
        })
      })
  },
  watch: {
    nameFilter (value) {

    }
  },
  computed: {
    filterByInput () {
      return this.filterProductsByFoodPairing(this.filterProductsByDescription(this.filterProductsByName(this.beers)))
    }
  },
  methods: {

    filterProductsByName (beers) {
      return beers.filter(filteredBeers => {
        return filteredBeers.name.toLowerCase().includes(this.nameFilter.toLowerCase())
      })
    },
    filterProductsByDescription (beers) {
      return beers.filter(filteredBeers => {
        return filteredBeers.description.toLowerCase().includes(this.descriptionFilter.toLowerCase())
      })
    },
    filterProductsByFoodPairing (beers) {
      return beers.filter(beer => {
        return beer.food_pairing.filter(food => {
          return food.toLowerCase().includes(this.foodPairingFilter.toLowerCase())
        }).length !== 0
      })
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
  background: radial-gradient(1.5em 6.28571em at 1.95em, rgba(255, 255, 255, 0) 50%, rgba(255, 255, 255, 0.25) 50%, rgba(255, 255, 255, 0.25) 55%, rgba(255, 255, 255, 0) 55%) 0 0, radial-gradient(1.5em 6.28571em at -0.45em, rgba(255, 255, 255, 0) 50%, rgba(255, 255, 255, 0.25) 50%, rgba(255, 255, 255, 0.25) 55%, rgba(255, 255, 255, 0) 55%) 1.5em 5.5em, radial-gradient(2.3em 4.57143em at 2.99em, rgba(255, 255, 255, 0) 50%, rgba(255, 255, 255, 0.3) 50%, rgba(255, 255, 255, 0.3) 55%, rgba(255, 255, 255, 0) 55%) 0 0, radial-gradient(2.3em 4.57143em at -0.69em, rgba(255, 255, 255, 0) 50%, rgba(255, 255, 255, 0.3) 50%, rgba(255, 255, 255, 0.3) 55%, rgba(255, 255, 255, 0) 55%) 2.3em 4em, radial-gradient(3.5em 6.28571em at 4.55em, rgba(255, 255, 255, 0) 50%, rgba(255, 255, 255, 0.25) 50%, rgba(255, 255, 255, 0.25) 55%, rgba(255, 255, 255, 0) 55%) 0 0, radial-gradient(3.5em 6.28571em at -1.05em, rgba(255, 255, 255, 0) 50%, rgba(255, 255, 255, 0.25) 50%, rgba(255, 255, 255, 0.25) 55%, rgba(255, 255, 255, 0) 55%) 3.5em 5.5em, radial-gradient(#15ffa5, #00ced1);
  background-color: mediumspringgreen;
  background-size: 1.5em 11em, 1.5em 11em, 2.3em 8em, 2.3em 8em, 3.5em 11em, 3.5em 11em, 100% 100%;
  background-repeat: repeat;
}
h1 {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: #bd7848;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}
label {
color: #bd7848;
text-shadow: 1px 1px 1px rgba(200, 200, 200, 1);
}
.inputs {
  flex: wrap;
}
input {
  max-width: 8em;
}
#container,
.container {
  width: 90%;
  margin: 0 auto;
  border: 5px solid #22c1c3;
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
  background: #2193b0;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to bottom, #6dd5ed, #2193b0);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to bottom, #6dd5ed, #2193b0); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  list-style: none;
}
#container .card {
  width: 300px;
  height:450px;
  color: #bd7848;
  border: 2px solid;
  font-size: 0,7em;
  transition: color 0.5s, border-color 0.5s, box-shadow 0.5s, transform 0.5s;
}
#container .card:hover {
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
.card{
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
ul>div {
  max-height: 70px;
}
p {
  max-height: 100px;
  overflow: auto;
}

button {
  max-width: 14em;
  min-width: 14em;
  background-color: #2193b0;
  border-radius: 2rem;
  border: 2px solid #2193b0;
  color: #6dd5ed;
}
.text-center {
  text-align: center;
}
h1 {
  text: 1.4em;
}
h2 {
  text: 1.3em;
  padding-top: 5px;
  padding-bottom: 5px;
}
h3 {
  text: 1.2em;
  padding-top: 5px;
  padding-bottom: 5px;
  margin-top: 5px;
  margin-bottom: 5px;
}
h4 {
  text: 1.1em;
  padding-top: 5px;
  padding-bottom: 5px;
  margin-top: 5px;
  margin-bottom: 5px;
}
p {
  text: 0.9em;
  padding-top: 5px;
  padding-bottom: 5px;
  margin-top: 5px;
  margin-bottom: 5px;
}
@media (min-width: 400px){
  h1 {
  text: 1.2em;
  }
  h2 {
  text: 1.1em;
  }
  h3 {
    text: 1.0em;
  }
  h4 {
    text: 0.9em;
  }
  p {
    text: 0.7em;
  }
}
</style>
