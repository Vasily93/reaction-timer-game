<template>
  <h1>Reaction Game Timer</h1>
  <button v-if="!isPlaying" @click="start">Play</button>
  <Block v-if="isPlaying" :delay="delay"/>
</template>

<script>
import Block from './components/Block.vue'
export default {
  name: 'App',
  components: { Block },
  data() {
    return {
      isPlaying: false,
      delay: null
    }
  },
  methods: {
    start() {
      this.delay = Math.floor(2000 + Math.random() * 5000)
      this.isPlaying = true
      console.log(this.delay)
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
</style>
