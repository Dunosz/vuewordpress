<template>
  <div class="container" v-if="menu">
    <div class="card" v-if="isLoading">Pobieram ofertę</div>
    <div class="card" v-for="item in checkValidDate" :key="item.id">
      <single-offer
        :date="item.acf.data"
        :soup="item.acf.zupa"
        :main="item.acf.drugie_danie"
        :price="item.acf.cena"
      />
    </div>
  </div>
</template>

<script>
import SingleOffer from "./SingleOffer.vue";
export default {
  components: { SingleOffer },
  data() {
    return {
      menu: null,
      isLoading: false,
    };
  },
  mounted() {
    this.fetchOffer();
  },
  methods: {
    // pobranie danych z Wordpress Rest API z użyciem ACF
    async fetchOffer() {
      this.isLoading = true;
      await fetch("https://vue.righthos.webd.pro/wp-json/wp/v2/oferty?_fields=acf")
        .then((response) => response.json())
        .then((data) => (this.menu = data));
      this.isLoading = false;
    },
    // funkcja na potrzebę sprawdzenia różnicy w dniach
    checkDayDiffrence(futureDate){
        let currentDay = new Date()
        let futureDay = new Date(futureDate)
        const oneDay = 1000*60*60*24
        const diffrence = futureDay.getTime()- currentDay.getTime();
        const diffrenceDays = Math.round(diffrence / oneDay);
        return diffrenceDays
    }
  },
    computed: {
      // sprawdzamy, czy róznica między datami znajduje się w zakresie od 7 dni do -1 (zastosowanie -1 pozwala na wyświetlanie oferty z bieżącego dnia)
        checkValidDate(){
            let filteredMenu = this.menu.filter(item => this.checkDayDiffrence(item.acf.data) <= 7 && this.checkDayDiffrence(item.acf.data) >= -1 )
            return  filteredMenu
        }
    }
};
</script>
<style>
.container {
  display: flex;
  align-content: center;
  align-items: center;
  flex-direction: column;
  justify-content: space-around;
}
.card {
  color: inherit;
  padding: 20px;
  text-align: center;
  border-radius: 10px;
  margin-bottom: 2em;

}
.title{
  border-bottom: 2px dotted inherit;
}
p {
    margin: 5px 0;
}
</style>
