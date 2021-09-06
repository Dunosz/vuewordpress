<template>
  <div id="app">
    <offer-box />
  </div>
</template>

<script>
import OfferBox from './components/OfferBox.vue'

export default {
  name: 'App',
  components: {
    OfferBox
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500&display=swap');
#app {
  font-family: Roboto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 16px;
  margin-top: 60px;
}
</style>
