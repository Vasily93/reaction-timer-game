<template >
  <p class='results'>
      <span class="player-count">Left: {{left}}</span>
      <strong>Round: {{round}}</strong>   
      <span class="player-count">Right: {{right}}</span>
  </p>
  <h3 class='results' v-if="finalWinner">
      {{this.finalWinner}}
  </h3>
</template>

<script>
export default {
    props: ['winner', 'setWinnerToNull', 'round'],
    data() {
        return {
            left: 0,
            right: 0,
            finalWinner: null
        }
    },
    methods: {
        setFinalWinner() {
            if(this.right > this.left) {
                this.finalWinner = 'Right player is the Winner'
            } else if(this.right < this.left) {
                this.finalWinner = 'Left player is the Winner'
            } else {
                this.finalWinner = 'This is a tie. Try again!'
            }
        }
    },
    watch: {
        round: function(val, oldVal) {
            if(val === 10) this.setFinalWinner()

            if(oldVal === 10 && val === 0) {
                this.right = 0
                this.left = 0
                this.finalWinner = null
            }
        },
        winner: function(val) {
            if(val !== null) {
                this.$data[this.winner] += 1
                this.setWinnerToNull()
            }
        }
    },
    updated() {

    }
}
</script>

<style>
    .results {
        background-color: rgb(255, 255, 255);
        margin: 20px 20%;
        padding: 10px;
        border-radius: 5px;
        
    }
    .player-count {
        margin: 0 80px;
    }
</style>