<template>
<div class="card">
  <h3>{{name}}</h3>
  <h4>"{{tagline}}"</h4>
  <div class="text-center">
    <div>
      <img :src="imageUrl">
    </div>
    <div>
        <button @click="toggleVisibility">{{ !visibility ? 'Show' : 'Hide'}}  food pairing</button>
      <div v-if="visibility">
        <div v-for="(food, i) in foodPairing" :key="i">
          <p>{{food}}</p>
        </div>
      </div>
    </div>
    <button @click="toggleVisibility">{{ visibility ? 'Show' : 'Hide'}} description</button>
    <p v-if="!visibility"> {{description}}</p>
  </div>
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
