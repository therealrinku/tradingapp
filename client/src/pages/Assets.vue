<template>
  <table class="trade-table">
    <thead>
      <tr>
        <th>Asset Name</th>
        <th>Current Price</th>
        <th>Quantity</th>
        <th>Total Value</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="asset in myAssets" :key="asset.name">
        <td>
          {{ asset.name }} <span style="font-weight:bold;font-size:10px;">{{ asset.symbol }}</span>
        </td>
        <td>${{ asset.price }}</td>
        <td>{{asset.quanity}}</td>
        <td>${{asset.quanity*asset.price}}</td>
        <div class="actions">
          <button @click="toggleTradeModal('Sell',asset.symbol)">Sell</button>
        </div>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "AssetsPage",
  props:{
      toggleTradeModal:Function,
      myAssets:Array
  },
};
</script>

<style scoped>
table {
  width: 85%;
  margin: auto;
  margin-top: 200px;
  border: solid 1px rgba(0, 0, 0, 0.2);
  border-radius: 5px;
  border-collapse: collapse;
  box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.2);
  border-style: hidden;
}

th {
  color: coral;
}
table,
tr,
td,
th {
  text-align: left;
  padding: 10px;
}
tr {
  border-bottom:solid 1px rgba(0, 0, 0, 0.1);
}
th {
  font-weight: normal;
  text-transform: uppercase;
  
}
th {
  font-size: 13px;
}
td {
  font-size: 14px;
}

.actions {
  display: flex;
  margin-top: 3px;
  align-items: center;
}

.actions button {
  border: none;
  background: inherit;
  width: 80px;
  text-align: center;
  height: 30px;
}

.actions button {
  background: coral;
  color: white;
  border-radius:5px;
  padding:10px 15px;
  width:35%;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
}

.actions button:hover{
  background:red;
}

</style>