<template>
  <CartaTable> </CartaTable>
</template>

<script>
import CartaTable from "~/components/organisms/CartaTable.vue";

export default {
  name: "App",
  components: {
    CartaTable,
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
  margin-top: 60px;
}
</style>
