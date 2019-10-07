<template>
  <div id="app">
    <NavBar></NavBar>
    <Product :premium="premium"></Product>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import NavBar from './components/layout/NavBar.vue';
import Product from './components/Product.vue';

@Component({
  components: {
    NavBar,
    Product,
  },
})
export default class App extends Vue {
  private premium = false;
}
</script>

<style>
#app {
  font-family: tahoma;
  color:#282828;
  margin: 0px;
}

  
</style>