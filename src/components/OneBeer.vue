<template>
<div class="flex-container">
  <li class="card">
  <h2>{{name}}</h2>
  <img :src="imageUrl">
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
    }
  },
  data () {
    return {
    }
  },
  methods: {
  }
}
</script>
<style>

.flex-container {
  display: flex;
  flex-wrap: wrap;

}

.card {
  width: 30%;
  height: 40%;
}
</style>
