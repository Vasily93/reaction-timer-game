<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
      <h1>{{ text }}</h1>
  </div>
</template>

<script>
export default {
    props: ['delay', 'player', 'letterKey'],
    data() {
        return {
            text: 'Click Me',
            showBlock: false,
            timer: null,
            reactionTime: 0
        }
    },
    watch: {
        delay: function(val, oldVal) {
            val !== oldVal ? this.showBlock = false : null
            this.initiate()
        }
    },
    methods: {
        initiate() {
            setTimeout(() => {
            this.chooseLetter()
            this.showBlock = true
            this.startTimer()
        }, this.delay) 
        },
        chooseLetter() {
            this.text = this.letterKey
        },
        startTimer() {
            this.timer = setInterval(() => {
                this.reactionTime += 10
            }, 10);
        },
        stopTimer() {
            clearInterval(this.timer)
            this.$emit('result', this.player)
        }
    },
    mounted() {
        this.initiate()
    },
    updated() {
        
    }
 
}
</script>

<style>
    .block {
        width: 200px;
        border-radius: 20px;
        background: linear-gradient(
            45deg,
            rgb(134, 65, 0) 0%,
            rgb(248, 192, 6) 60%
        );
        text-align: center;
        padding: 70px 0;
        margin: 40px auto;
        color: white;
        border: solid;
        border-width: 5px;
        
    }
</style>