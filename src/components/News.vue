<template>
  <div class="news">
      <h2>Promethium News</h2>
      <div class="twitter" v-if="twitterOn">
          <!-- <Timeline id="ChainPromethium" sourceType="profile" :options="{ tweetLimit: '5' }"/> -->
      </div>
      
      <!-- <Timeline id="ChainPromethium" sourceType="likes" :options="{ theme: 'dark' }"/> -->
      <!-- <Timeline id="ChainPromethium" sourceType="list" /> -->
  </div>
</template>

<script>
// import { Timeline } from 'vue-tweet-embed'
export default {
    components: {
        // Timeline
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