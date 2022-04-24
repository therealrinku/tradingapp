<template>
  <nav class="topbar">
    <div>
      <p style="margin-right:30px;">Balance:{{ !assetValueHidden ? "$" + this.currentBalance : "**" }}</p>
      <p>Assets Value:{{ !assetValueHidden ? "$" + assetsValue : "**" }}</p>
      <button @click="toggleAssetValueView()">
        {{ assetValueHidden ? "Show" : "Hide" }}
      </button>
      <p style="margin-left: 25px; font-weight: bold">{{ this.username }}</p>
      <button>Logout</button>
    </div>
  </nav>
</template>

<script>
export default {
  name: "TopBar",
  props: {
    username:String,
    currentBalance:Number,
    assets:Array,
  },
  data() {
    return {
      assetValueHidden: false,
      assetsValue:100
    };
  },
  methods: {
    toggleAssetValueView() {
      this.assetValueHidden = !this.assetValueHidden;
    },
  },
};
</script>

<style scoped>
.topbar {
  border-bottom: solid 1px rgba(0, 0, 0, 0.1);
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 25px;
  font-family: monospace;
}

.topbar div {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  height: 100%;
  max-width: 98%;
}
.topbar button {
  border: none;
  background: inherit;
  text-decoration: underline;
}
</style>
