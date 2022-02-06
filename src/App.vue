<template>
  <h1>Reaction Game Timer</h1>
  <button v-if="!isPlaying && round !== 10" @click="start">Start Playing</button>
  <button v-if="round === 10" @click="startover">Start Over</button>
  <Results :winner="winner" 
    :setWinnerToNull="setWinnerToNull"
    :round="round"
  />
  <div class="players" v-if="isPlaying">
    <Block
      :delay="delay"
      player="left"
      :letterKey="leftKey"
      
    />
    <Block
      :delay="delay"
      player="right"
      :letterKey="rightKey"
      
    />
  </div>
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'
export default {
  name: 'App',
  components: { Block, Results },
  data() {
    return {
      isPlaying: false,
      delay: null,
      letters: [['A', 'S', 'D', 'F'], ['H', 'J', 'K', 'L']], 
      leftKey: null,
      rightKey: null,
      winner: null,
      round: 0
    }
  },
  watch: {
    round: function(val) {
      if( val !== 10) {
        this.start()
      }
    }
  },
  methods: {
    start() {
      this.delay = Math.floor(2000 + Math.random() * 5000)
      this.setLetters()
      this.isPlaying = true
    },
    startover() {
      this.round = 0
    },
    setLetters() {
      this.letters.map((arr, i) => {
      if(i === 0) {
        this.leftKey = arr[Math.floor(Math.random() * 3)]
      } else if(i === 1) {
        this.rightKey = arr[Math.floor(Math.random() * 3)]
      }
      })
    },
    handleKeyPress(letter) {
      if(letter === this.leftKey || letter === this.rightKey) {
        if(letter === this.leftKey)this.winner = 'left' 
        if(letter === this.rightKey) this.winner = 'right'
        this.round += 1
        this.isPlaying = false
      }
    },
    setWinnerToNull() {
      this.winner = null
    }
  },
  mounted() {
    document.addEventListener('keydown', (e) => {
      this.handleKeyPress(e.code[e.code.length-1])
      
    })
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
.players {
  display: inline;
}
</style>
