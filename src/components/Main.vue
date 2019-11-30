<template>
    <div class="main">
        <h2 class="apptitle">iPromethium v0.1</h2>
        <v-btn @click="close()" class="mx-2 close" fab dark x-small color="pink">
          <span>X</span>
        </v-btn>
        <v-btn @click="minimize()" class="mx-2 minimize" fab dark x-small color="green">
          <span>_</span>
        </v-btn>
        <v-container>
            <v-row>
                <v-col :cols="3">
                    <div class="date">{{ this.dateNow }}</div>
                    <v-btn @click="setMain()" id="pcm" outlined color="cyan" class="menubtn ma-2">Promethium</v-btn>
                    <v-btn @click="setCoins()" id="coins" outlined color="cyan" class="menubtn ma-2">Coins</v-btn>
                    <v-btn @click="setMarket()" id="market" outlined color="cyan" class="menubtn ma-2">Market</v-btn>
                    <v-btn @click="setNews()" id="news" outlined color="cyan" class="menubtn ma-2">News</v-btn>
                </v-col>
                <v-col :cols="9">
                    <Promethium ref="promethiumComponent" v-bind:btcPrice="btcPrice" v-if="mainOn" />
                    <Coins  v-if="coinsOn" />
                    <Market v-if="marketOn" />
                    <News v-if="newsOn" />
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>


<script>
import axios from 'axios'
import Promethium from './Promethium'
import Coins from './Coins'
import Market from './Market'
import News from './News'
export default {
  components: {
    Promethium,
    Coins,
    Market,
    News
  },
  data () {
    return {
      btcPrice: '',
      mainOn: true,
      coinsOn: false,
      marketOn: false,
      newsOn: false,
      dateNow: ''
    }
  },
  mounted () {
    var d = new Date()
    var c = d.toString().split('GMT')
    this.dateNow = c[0]
    this.getBtcPrice()
  },
  methods: {
    getBtcPrice () {
      var btcURL = 'https://api.coindesk.com/v1/bpi/currentprice.json'
      axios.get(btcURL)
        .then(response => {
          var p = response.data.bpi.USD.rate.replace(',', '')
          var f = parseFloat(p)
          this.btcPrice = f.toFixed(2)
          this.$refs.promethiumComponent.pcmInit()
        })
        .catch(err => {
          alert('error getting btc price from api : ' + err)
          
        })
    },
    setMain () {
      this.$refs.promethiumComponent.pcmInit()
      this.mainOn = true
      this.coinsOn = false
      this.marketOn = false
      this.newsOn = false
    },
    setCoins () {
      this.mainOn = false
      this.coinsOn = true
      this.marketOn = false
      this.newsOn = false
    },
    setMarket () {
      this.marketOn = true
      this.mainOn = false
      this.coinsOn = false
      this.newsOn = false
    },
    setNews () {
      this.newsOn = true
      this.mainOn = false
      this.coinsOn = false
      this.marketOn = false
    },
    close () {
      let w = this.getCurrentWindow()
      w.close()
    },
    minimize () {
      let w = this.getCurrentWindow()
      w.minimize()
    },
    getCurrentWindow () {
      const remote = require('electron').remote
      let w = remote.getCurrentWindow()
      return w 
    }
  }
}
</script>

<style>

* {
  text-align: center;
  color: rgb(0, 0, 0);
  font-size: 14px;
  -webkit-app-region: drag;
}


.menubtn {
    width: 150px;
}
.date {
    margin-bottom: 10px;
    font-size: 12px;
}

.apptitle {
    height: 0px;
    text-decoration: underline;
}

.close {
  position: absolute;
  top: 5px;
  left: 850px;
}

.minimize {
  position: absolute;
  top: 5px;
  left: 815px;
}

</style>