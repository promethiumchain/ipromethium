<template>
  <div class="news">
      <h2>Promethium News</h2>
      <div class="twitter" v-if="twitterOn">
        <twitter>
            <div slot="loading">loading .....</div>
            <a class="twitter-timeline" href="https://twitter.com/ChainPromethium?ref_src=twsrc%5Etfw">Tweets by Promethium Chain Team</a>
        </twitter>      
      </div>
  </div>
</template>

<script>
export default {
    components: {
    },
    data () {
        return {
            twitterOn: false,
        }
    },
    mounted () {
        this.twitterOn = true
    }
}
</script>

<style>

</style>