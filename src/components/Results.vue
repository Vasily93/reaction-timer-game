<template>
  <p v-if="!finalWinner">Left: {{left}}  Right: {{right}} Round: {{round}}</p>
  <h3 v-if="finalWinner">{{this.finalWinner}}</h3>
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
                this.finalWinner = 'Right is the Winner'
            } else if(this.right < this.left) {
                this.finalWinner = 'Left is the Winner'
            } else {
                this.finalWinner = 'This is a draw'
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

</style>