<template>
  <nav class="navbar">
    <div>
        <button @click="this.changeCurrentPage('trade')" :style="[this.currentPage==='trade'?{borderBottom:'solid 2px coral'}:{}]">Trade</button>
        <button @click="this.changeCurrentPage('assets')" :style="[this.currentPage==='assets'?{borderBottom:'solid 2px coral'}:{}]">My Assets</button>
        <button @click="this.changeCurrentPage('settings')" :style="[this.currentPage==='settings'?{borderBottom:'solid 2px coral'}:{}]">Settings</button>
    </div>
  </nav>
</template>

<script>
export default {
  name: "NavBar",
  props:{
    currentPage:String,
    changeCurrentPage:Function
  }
};
</script>

<style scoped>
.navbar {
  border-bottom: solid 1px rgba(0, 0, 0, 0.1);
  position: fixed;
  top: 26px;
  left: 0;
  width: 100%;
  height: 45px;
}

.navbar div {
  display: flex;
  align-items: center;
  justify-content:center;
  height: 100%;
  max-width:95%;
}

.navbar button {
  height: 100%;
  width: 200px;
  background: inherit;
  border: solid 1px rgba(0, 0, 0, 0.1);
  border-bottom: none;
  border-top: none;
  border-right: none;
}

.navbar button:last-child {
  border-right: solid 1px rgba(0, 0, 0, 0.1);
}
</style>
