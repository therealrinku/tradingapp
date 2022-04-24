<template>
  <div class="overlay" @click="toggleTradeModal(null)"></div>
  <div class="buy-sell-modal">
    <p>{{ tradeMode + " " + assetName}} </p>
    <p>{{assetName}} is a cryptop currency which is very popular lol.</p>
    <div class="actions">
        <button @click="setQuantity('-1')" :disabled="[quantity===0?true:false]">-</button>
        <input type="number" v-model="quantity" />
        <button @click="setQuantity('+1')" :disabled="[quantity===99?true:false]">+</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TradeModal",
  data(){
      return {
          quantity:0
      }
  },
  methods:{
      setQuantity(value){
          if(value==="+1"){
              return this.quantity=this.quantity+1
          }
          if(value==="-1"){
              return this.quantity=this.quantity-1
          }
          this.quantity=value
          
      }
  },
  props: {
    tradeMode: String,
    assetName:String,
    toggleTradeModal:Function
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
  top:0;
  left: 0;
}
.buy-sell-modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  background: white;
  z-index: 2;
  height: 300px;
  width: 300px;
  padding:10px 15px;
  border-radius:10px;
}

input{
    text-align:center;
    border:solid 1px rgba(0, 0, 0, 0.2);
    margin:0 5px;
    height:25px;
    outline:none;
}

button{
    border:solid 1px rgba(0, 0, 0, 0.2);
    height:29px;
    width:30px;
}
</style>