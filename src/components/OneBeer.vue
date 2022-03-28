<template>
<div class="">
  <li class="card">
  <h2>{{name}}</h2>
  <h3>"{{tagline}}"</h3>
  <div class="text-center">
    <div>
      <img :src="imageUrl">
    </div>
    <div>
        <button @click="toggleVisibility">{{ !visibility ? 'Show' : 'Hide'}}  food pairing</button>
      <ul v-if="visibility">
        <div v-for="(food, i) in foodPairing" :key="i">
          <p>{{food}}</p>
        </div>
      </ul>
    </div>
    <button @click="toggleVisibility">{{ visibility ? 'Show' : 'Hide'}} description</button>
    <p v-if="!visibility"> {{description}}</p>
  </div>
  </li>
</div>
</template>

<script>

export default {
  props: {
    id: {
      type: Number,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    imageUrl: {
      type: String,
      required: true
    },
    tagline: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: true
    },
    foodPairing: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      visibility: true
    }
  },
  methods: {
    toggleVisibility () {
      this.visibility = !this.visibility
    }
  }
}
</script>
<style>
</style>
