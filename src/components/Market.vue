<template>
  <div class="market">
      <h2>Explore The Promethium Network P2P Market</h2>
      <div class="games" v-for="(game, index) in games" :key="index" >
          <v-btn outlined color="cyan" class="game ma-2">
              {{ game.name }}
          </v-btn>
      </div>
  </div>
</template>

<script>
export default {
    name: "Market",
    data () {
        return {
          games: [
                {
                  id: '0',
                  name: 'CSGO',
                  prefix: 'CSGO_'
                },
                {
                  id: '1',
                  name: 'Dota2',
                  prefix: 'DOTA2_'
                }
            ]
        }
    }
}
</script>

<style>
.game {
    width: 80%;
    margin-bottom: 10px;
}

h2 {
    margin-bottom: 10px;
}

</style>