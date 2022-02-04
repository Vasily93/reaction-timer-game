<template>
  <div class="block" v-if="showBlock" @click="hide">
      Click Me
  </div>
</template>

<script>
export default {
    props: ['delay', 'id', 'letters'],
    data() {
        return {
            showBlock: false
        }
    },
    methods: {
        hide() {
            console.log('clicking the block')
            this.showBlock = false
        }
    },
    mounted() {
        setTimeout(() => {
            this.showBlock = true
        }, this.delay)
    }
}
</script>

<style>
    .block {
        width: 400px;
        border-radius: 20px;
        background: goldenrod;
        columns: white;
        text-align: center;
        padding: 100px 0;
        margin: 40px auto;
    }
</style>