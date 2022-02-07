<template>
  <h1 class='game-name'>Reaction Game Timer</h1>
  <Results :winner="winner" 
    :setWinnerToNull="setWinnerToNull"
    :round="round"
  />
  <button v-if="!isPlaying && round !== 10" @click="start">Start Playing</button>
  <button v-if="round === 10" @click="startover">Start Over</button>
  <div class='rules' v-if="!isPlaying">
    <span>
      <p>This game is for 2 players. Each player gets 4 letters.</p>
      <p>Player on the left: A, S, D, F.</p>
      <p>Player on the right: H, J, K, L.</p>
      <p>Within few seconds after starting the game  a card will appear on each side.
        Whoever hits the right letter on their side faster wins the round.
      </p>
      <p>The game is 10 rounds.</p>
    </span>
  </div>
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
      console.log(e.code)
      this.handleKeyPress(e.code[e.code.length-1])
      
    })
  }
}
</script>

<style>
body, html {
  height: 100%;
  
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50d7;
  height: 100%;
  width: 100%;
  background: linear-gradient(
    95deg,
    rgb(4, 45, 65) 0%,
    rgba(179, 229, 252, 1) 50%,
    rgb(255, 145, 0) 50%,
    rgb(98, 131, 240) 100%
  );
}
.game-name {
  background-color: rgb(255, 255, 255);
  margin: 0 20%;
  border-radius: 0 0 10px 10px;

}
.players {
  display: flex;
  flex-direction: row;
}
button {
  padding: 10px 10px;
  background-color: rgb(134, 134, 238);
  border-radius: 5px;
  border: none;
  color: white;
}
.rules {
  background-color: rgba(2, 2, 34, 0.466);
  color: white;
  font-size: large;
  margin: 50px 20%;
  padding: 10px;
  border-radius:  10px;
}
</style>
