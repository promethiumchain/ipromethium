<template>
  <div>
    <v-alert
      v-model="alert"
      border="left"
      close-text="Close Alert"
      color="deep-purple accent-4"
      dark
      dismissible
    >
    {{ }}
    </v-alert>
    <div class="text-center">
      <v-btn
        v-if="!alert"
        color="deep-purple accent-4"
        dark
        @click="alert = true"
      >
        Reset
      </v-btn>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>