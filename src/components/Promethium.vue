<template>
  <div class="promethium">
      <h3>Promethium Network Stats</h3>
      <img src="../assets/crystal.png"  class="crystal">
      <div class="blocknumber">
        Current Block Number : {{ this.pcmBlockNumber}}
      </div>
      <div class="hashrate">
          Promethium Global Hashrate : {{ this.pcmHashrate }} MH/s
      </div>
      <div class="diff">
          Promethium Difficulty : {{ this.pcmDiff }}
      </div>
      <div class="costpercoin">
          Promethium Cost Per Coin To Make in USD : {{ this.pcmPrice }} USD
      </div>
      <div class="pcmbtcprice">
          Promethium Cost Per Coin To Make in BTC : {{ this.pcmBtcPrice }} Sats
      </div>
  </div>
</template>

<script>
import Pcm from 'web3-eth'
export default {
  props: ['btcPrice'],
  data () {
    return {
      pcmBlockNumber: '',
      pcmPrice: '',
      pcmBtcPrice: '',
      pcmHashrate: '',
      pcmDiff: '',
      isInit: true
    }
  },
  methods: {
    pcmInit () {
      this.getPcmData()
    },
    getPcmData () {
      var pcm = new Pcm('ws://209.250.240.205:9989')
      pcm.getBlock('latest')
        .then(response => {
          this.pcmBlockNumber = response.number
          var diff = response.difficulty
          var hashrate = (diff / 14) / 1000000
          const coinsPerDay = 7200 * 3
          const sixCoreSystemHashrate = 0.5
          var coinsPerDaySixCoreSystem = (sixCoreSystemHashrate * coinsPerDay) / hashrate
          var costPerCoin = 120 / (30 * coinsPerDaySixCoreSystem)
          const satoshiesPerBtc = 100000000
          var costPerPcmBtc = (costPerCoin * satoshiesPerBtc) / this.btcPrice
          var fprice = costPerPcmBtc / satoshiesPerBtc
          var priceInSatoshies = fprice.toFixed(8)
          this.pcmPrice = costPerCoin.toFixed(3)
          this.pcmBtcPrice = priceInSatoshies
          this.pcmHashrate = hashrate.toFixed(3)
          this.pcmDiff = diff
          this.isInit = true
        })
        .catch(err => alert('error connecting to the promethium network' + err))
    }
  },
  mounted () {
    if(!this.isInit) {
      return
    } else {
      this.getPcmData()
    }
  }
}
</script>

<style>

.crystal {
  height: 100px;
  width: auto;
  filter: grayscale();
}
</style>