<template>
  <input v-bind:value="cValue" v-on:input="inputHandle">
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      cValue: ''
    }
  },
  methods: {
    inputHandle ($event) {
      console.log($event.target.value)
      this.cValue = $event.target.value
    },
    getDate () {
      return this.cValue
    }
  }
}
</script>

<style>
#app {
  
}
</style>
