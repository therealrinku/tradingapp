<template>
  <TopBar :username="username" :currentBalance="currentBalance" :assets="myAssets"/>
  <NavBar :currentPage="currentPage" :changeCurrentPage="changeCurrentPage" />
  <div v-if="currentPage === 'trade'">
    <TradePage :toggleTradeModal="toggleTradeModal" :assets="assets" />
  </div>
  <div v-if="currentPage === 'assets'">
    <AssetsPage :toggleTradeModal="toggleTradeModal" :myAssets="myAssets" />
  </div>
  <div v-if="showTradeModal">
    <TradeModal
      :assetName="assetName"
      :tradeMode="tradeMode"
      :toggleTradeModal="toggleTradeModal"
      :totalBalance="currentBalance"
      :pricePerCoin="assets.filter(a=>a.symbol===assetName)[0].price"
      :noOfCoins="myAssets.filter(a=>a.symbol===assetName)[0]?.quanity || 0"
      :performTrade="performTrade"
    />
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
  data() {
    return {
      currentPage: "trade",
      username: "Jane Doe",
      currentBalance: 50,
      showTradeModal: false,
      tradeMode: null,
      assetName: null,
      assets: [
        { name: "Cardano", price: "0.95", symbol: "ADA" },
        { name: "Bitcoin", price: "42,454", symbol: "BTC" },
        { name: "Shiba INU", price: "0.000029", symbol: "SHIB" },
        { name: "Avalanche", price: "98.44", symbol: "AVAX" },
        { name: "Tron", price: "0.0092", symbol: "TRX" },
        { name: "Solana", price: "99.34", symbol: "SOL" },
        { name: "Dogecoin", price: "0.29", symbol: "DOGE" },
        { name: "Squid Games", price: "0.000004", symbol: "SQUID" },
        { name: "Scam INU", price: "0.000000000034939", symbol: "SCAM" },
      ],
      myAssets: [
        { name: "Cardano", price: 0.95, symbol: "ADA", quanity: 43 },
        { name: "Bitcoin", price: 42454, symbol: "BTC", quanity: 35.55 },
        { name: "Shiba INU", price: 0.000029, symbol: "SHIB", quanity: 24.34 },
        { name: "Avalanche", price: 98.4, symbol: "AVAX", quanity: 204.45 },
        { name: "Solana", price: 99.34, symbol: "SOL", quanity: 390.44 },
      ],
    };
  },
  methods: {
    changeCurrentPage(pageName) {
      this.currentPage = pageName;
    },
    toggleTradeModal(tradeMode, assetName) {
      this.showTradeModal = !this.showTradeModal;
      this.tradeMode = tradeMode;
      this.assetName = assetName;
    },
    performTrade(data){
        const updatedMyAssets=[...this.myAssets];
        const updatedAssetIndex=updatedMyAssets.findIndex(d=>d.symbol===data.assetSymbol);
        updatedMyAssets[updatedAssetIndex].quanity=data.updatedAssetQuantity;
        this.currentBalance=data.updatedBalance;
        this.myAssets=updatedMyAssets;
        this.showTradeModal=false;
    }
  },
  components: {
    NavBar,
    TradePage,
    TopBar,
    AssetsPage,
    TradeModal,
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

button:hover {
  cursor: pointer;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type="number"] {
  -moz-appearance: textfield;
}

button:disabled:hover {
  cursor: not-allowed;
}

button:disabled {
  opacity: 0.6;
}
</style>
