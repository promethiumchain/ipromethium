<template>
  <v-app>
    <Main />
  </v-app>
</template>

<script>
import Main from './components/Main'

export default {
  name: 'App',

  components: {
    Main,
  },

  data: () => ({
    //
  }),
}
</script>

<style>
::-webkit-scrollbar {
    display: none;
}
</style>