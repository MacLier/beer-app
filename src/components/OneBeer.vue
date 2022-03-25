<template>
  <li :style="{'background-image': 'url(' + imageUrl +')'}"
  class="card">
  <h2>{{name}}</h2>
  </li>
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
