<template>
  <TopBar :username="username" :currentBalance="currentBalance"/>
  <NavBar :currentPage="currentPage" :changeCurrentPage="changeCurrentPage"/>
  <div v-if="currentPage==='trade'">
    <TradePage :toggleTradeModal="toggleTradeModal"/>
  </div>
  <div v-if="currentPage==='assets'">
    <AssetsPage :toggleTradeModal="toggleTradeModal"/>
  </div>
  <div v-if="showTradeModal">
    <TradeModal :assetName="assetName" :tradeMode="tradeMode" :toggleTradeModal="toggleTradeModal"/>
  </div>
  <link
    href="https://cdn.jsdelivr.net/npm/@mdi/font@6.x/css/materialdesignicons.min.css"
    rel="stylesheet"
  />
</template>

<script>
import TopBar from "./components/Topbar.vue";
import NavBar from "./components/Navbar.vue";
import TradePage from "./pages/Trade.vue";
import AssetsPage from "./pages/Assets.vue";
import TradeModal from "./components/TradeModal.vue";

export default {
  name: "App",
  data(){
    return {
      currentPage:"trade",
      username:"Jane Doe",
      currentBalance:"$50",
      showTradeModal:false,
      tradeMode:null,
      assetName:null,
    }
  },
  methods:{
    changeCurrentPage(pageName){
      this.currentPage=pageName
    },
    toggleTradeModal(tradeMode,assetName){
      this.showTradeModal=!this.showTradeModal
      this.tradeMode=tradeMode
      this.assetName=assetName
    }
  },
  components: {
    NavBar,
    TradePage,
    TopBar,
    AssetsPage,
    TradeModal
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

html,
body {
  margin: 0;
}

button:hover{
  cursor: pointer;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type=number] {
  -moz-appearance: textfield;
}

button:disabled:hover{
  cursor:not-allowed;
}

button:disabled{
  opacity: 0.6;
}
</style>
