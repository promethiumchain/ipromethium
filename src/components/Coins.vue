<template>
  <div class="coins">
      <h2> Coin Prices Right Now </h2>
      <div class="wraper inventory">
          <div class="inv-item" v-for="(coin, index) in coinPrices" v-bind:key="index">
                <v-row>
                    <v-col :cols="12">
                        <div class="coinname">
                            {{ coin.coinName }}
                        </div>
                    </v-col>
                    <v-col class="priceleft" :cols="4">
                         <div class="usdprice">
                            {{ coin.usdPrice }} USD
                        </div>
                        <div class="usd24h">
                            24H Change : {{ coin.usd24hChange }} USD
                        </div>
                    </v-col>
                    <v-col class="priceright" :cols="4">
                        <div class="eurprice">
                            {{ coin.eurPrice }} EUR 
                        </div>
                        <div class="eur24h">
                            24H Change : {{ coin.eur24hChange }} EUR
                        </div>
                    </v-col>
                </v-row>
          </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Coins',
  data () {
    return {
      coinPrices: []
    }
  },
  methods: {
    getCoinPrices () {
      var btcURL = 'https://api.coingecko.com/api/v3/simple/price?ids=bitcoin%2Clitecoin%2Cethereum%2Cdash%2Ctether&vs_currencies=usd%2Ceur&include_24hr_change=true'
      const forFixed = 2
      axios.get(btcURL)
        .then(response => {
          var data = response.data
          var btcusd24h = data.bitcoin.usd_24h_change
          var btceur24h = data.bitcoin.eur_24h_change
          var btc = {
            coinName: 'Bitcoin',
            usdPrice: data.bitcoin.usd,
            usd24hChange: btcusd24h.toFixed(forFixed),
            eurPrice: data.bitcoin.eur,
            eur24hChange: btceur24h.toFixed(forFixed)
          }
          var ltcusd24h = data.litecoin.usd_24h_change
          var ltceur24h = data.litecoin.eur_24h_change
          var ltc = {
            coinName: 'Litecoin',
            usdPrice: data.litecoin.usd,
            usd24hChange: ltcusd24h.toFixed(forFixed),
            eurPrice: data.litecoin.eur,
            eur24hChange: ltceur24h.toFixed(forFixed)
          }
          var ethusd24h = data.ethereum.usd_24h_change
          var etheur24h = data.ethereum.eur_24h_change
          var eth = {
            coinName: 'Ethereum',
            usdPrice: data.ethereum.usd,
            usd24hChange: ethusd24h.toFixed(forFixed),
            eurPrice: data.ethereum.eur,
            eur24hChange: etheur24h.toFixed(forFixed)
          }
          var dashusd24h = data.dash.usd_24h_change
          var dasheur24h = data.dash.eur_24h_change
          var dash = {
            coinName: 'Dash',
            usdPrice: data.dash.usd,
            usd24hChange: dashusd24h.toFixed(forFixed),
            eurPrice: data.dash.eur,
            eur24hChange: dasheur24h.toFixed(forFixed)
          }
          var tetherusd24h = data.tether.usd_24h_change
          var tethereur24h = data.tether.eur_24h_change
          var tether = {
            coinName: 'Tether',
            usdPrice: data.tether.usd,
            usd24hChange: tetherusd24h.toFixed(forFixed),
            eurPrice: data.tether.eur,
            eur24hChange: tethereur24h.toFixed(forFixed)
          }
          this.coinPrices.push(btc)
          this.coinPrices.push(ltc)
          this.coinPrices.push(eth)
          this.coinPrices.push(dash)
          this.coinPrices.push(tether)
        })
        .catch(err => alert('error getting coin prices from api : ' + err))
    }
  },
  mounted () {
    this.getCoinPrices()
  }
}
</script>

<style scoped>

.coinname {
    position: relative;
    top: -10px;
    font-size: 10px;
}

.priceleft {
    position: relative;
    top: -30px;
    left: 30px;
}

.priceright {
    position: relative;
    top: -30px;
    left: 60px;
}

.usdprice, .eurprice {
    font-size: 10px;
    width: 100px;
}

.usd24h, .eur24h {
    font-size: 8px;
    width: 100px;
}

.inventory {
  display: grid;
  grid-template-columns: repeat(2, 300px);
  grid-template-rows: 60px 60px 60px;
  grid-column-gap: 5px;
  grid-row-gap: 5px;
  background: rgba(0, 0, 0, 0.01);
}

.inv-item {
    border: 1px solid rgb(255, 0, 179);
    
    padding: 0.1rem;
    border-radius: 3px;
}

h2 {
    margin-bottom: 15px;
}


</style>