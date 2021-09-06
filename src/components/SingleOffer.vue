<template>
  <div>
    <div class="header">Oferta na dzień: {{parseDate.day }}.{{parseDate.month + 1}}.{{parseDate.year}}</div>
    <div class="single-box" >
      <h3 class="title">Zupa</h3>
      <p>{{ soup }}</p>
      <h3 class="title">Drugie danie</h3>
      {{ main }}
      <h3 class="title">Cena</h3>
      <p class="price">{{ price }} PLN</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
      soup: String,
      main: String,
      price: String,
      date: String,
  },
  data() {
    return {
      menu: null,
      isLoading: false,
    };
  },
  computed: {
    parseDate(){
      let currentDay = new Date(this.date)
      return {day: currentDay.getDate(), month: currentDay.getMonth(), year: currentDay.getFullYear()}
    }
  }
};
</script>

<style scoped>
.single-box {
  width: 400px;
  height: 350px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: 1.2em;
}
.header {
  font-size: 1.5em;
  background-color: #E61313;
  color: aliceblue;
  padding: 20px;
}
.price {
  font-size: 2em;
}

</style>
