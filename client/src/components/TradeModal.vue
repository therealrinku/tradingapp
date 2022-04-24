<template>
  <div class="overlay" @click="toggleTradeModal(null)"></div>
  <div class="buy-sell-modal">
    <div class="trade-box" v-if="!previewMode">
      <div class="tabs">
        <button
          @click="setCurrentMode('Buy')"
          :style="[
            currentMode === 'Buy' ? { borderBottom: 'solid 2px #019267' } : {},
          ]"
        >
          Buy
        </button>
        <button
          @click="setCurrentMode('Sell')"
          :style="[
            currentMode === 'Sell' ? { borderBottom: 'solid 2px coral' } : {},
          ]"
        >
          Sell
        </button>
      </div>
      <p>{{ assetName + " Balance:" + noOfCoins }}</p>
      <p>{{ "Number of" + " " + assetName }}</p>
      <div class="actions">
        <input type="number" v-model="quantity" autofocus />
        <button
          class="main-action-button"
          @click="this.previewMode = true"
          :disabled="quantity<=0 || quantity>noOfCoins"
          :style="[currentMode === 'Sell' ? { background: 'coral' } : {}]"
        >
          Preview {{ currentMode }}
        </button>
      </div>
    </div>

    <div class="preview" v-if="previewMode">
      <span class="top-bar">
        <button class="back-button" @click="this.previewMode=false">Go Back</button>
        <p>{{currentMode+"ing "}} <b>{{assetName}}</b></p>
      </span>
      <p>Number of {{assetName}}: {{ quantity }}</p>
      <p>Price per Coin: {{pricePerCoin}}</p>
      <p>Total Price : {{ quantity * pricePerCoin }}</p>
      <p>Fees : 0</p>
      <p>New Balance : ${{ currentMode==="Buy" ? (50 - (quantity * pricePerCoin)) : (50 + (quantity * pricePerCoin)) }}</p>
      <p>New {{assetName}} Balance : {{ currentMode==="Buy" ? (noOfCoins + quantity) : (noOfCoins- quantity) }}</p>
      <button
        class="main-action-button"
        @click="performTrade({assetSymbol:assetName,updatedBalance:currentMode==='Buy' ? (50 - (quantity * pricePerCoin)) : (50 + (quantity * pricePerCoin)),updatedAssetQuantity:currentMode==='Buy' ? (noOfCoins + quantity) : (noOfCoins- quantity)})"
        :style="[currentMode === 'Sell' ? { background: 'coral',marginTop:'40px' } : {marginTop:'40px'}]"
      >
        {{ currentMode }} Now
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TradeModal",
  data() {
    return {
      quantity: 0,
      currentMode: this.tradeMode,
      previewMode: false,
    };
  },
  methods: {
    setQuantity(value) {
      if (value === "+1") {
        return (this.quantity = this.quantity + 1);
      }
      if (value === "-1") {
        return (this.quantity = this.quantity - 1);
      }
      this.quantity = value;
    },
    setCurrentMode(value) {
      this.currentMode = value;
    },
  },
  props: {
    tradeMode: String,
    assetName: String,
    toggleTradeModal: Function,
    totalBalance: Number,
    pricePerCoin: Number,
    noOfCoins: Number,
    performTrade: Function,
  },
};
</script>

<style scoped>
.overlay {
  position: fixed;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  z-index: 0;
  top: 0;
  left: 0;
}
.buy-sell-modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  z-index: 2;
  height: 300px;
  width: 300px;
  border-radius: 5px;
  font-size: 15px;
  padding: 10px;
}

input {
  text-align: center;
  border: solid 1px rgba(0, 0, 0, 0.2);
  height: 25px;
  outline: none;
  border-radius: 5px;
  font-size: 50px;
  height: auto;
  width: 98%;
}

.tabs {
  width: 100%;
  margin-bottom: 25px;
}

.tabs button {
  width: 50%;
  background: inherit;
  border: none;
  border-bottom: solid 1px rgba(0, 0, 0, 0.2);
  height: 30px;
  padding: 5px 10px;
}

.main-action-button {
  display: block;
  margin: auto;
  margin-top: 80px;
  background: #019267;
  color: white;
  border-radius: 5px;
  padding: 10px 15px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border: none;
}

.preview .top-bar{
  border-bottom:solid 1px rgba(0, 0, 0, 0.2);
  width:100%;
  height:20px;
  display:block;
  padding:3px 0 6px 0;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
}

.preview .back-button{
  position:absolute;
  left:5px;
  top:15px;
  border:none;
  background:none;
  text-decoration:underline;
}
</style>