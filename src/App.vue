<template>
  <div id="app">
    <NavBar></NavBar>
    <div class="product">
      <div class="product-image">
        <img :src="image" />
      </div>

      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inventory > 10">In Stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Almost out!</p>
        <p v-else>Out of Stock</p>

        <ul>
          <li v-for="detail in details" :key="detail">{{ detail }}</li>
        </ul>

        <div v-for="variant in variants" :key="variant.variantId">
          <p @mouseover="updateImage(variant.variantImage)">{{ variant.variantColor }}</p>
        </div>

        <button v-on:click="addToCart">Add to Cart</button>

        <div class="cart" ><p>Cart ({{ cart }})</p></div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import NavBar from './components/layout/NavBar.vue';

@Component({
  components: {
    NavBar,
  },
})
export default class App extends Vue {
  private product: string = 'Socks';
  private image = '';
  private inventory: number = 100;
  private details: string[] = ['80% cotton', '20% polyester', 'Gender-netral'];
  private variants: ProductVariant[] = [
      {
        variantId: 2234,
        variantColor: 'green',
        variantImage: '/img/vmSocks-green-onWhite.jpg',
      },
      {
        variantId: 2235,
        variantColor: 'blue',
        variantImage: '/img/vmSocks-blue-onWhite.jpg',
      },
    ];
  private cart: number = 0;

  constructor() {
    super();
    this.image = this.variants[0].variantImage;
  }

  private addToCart() {
    this.cart += 1;
  }

  private updateImage(img: string) {
    this.image = img;

  }
}

interface ProductVariant {
  variantId: number;
  variantColor: string;
  variantImage: string;
}

</script>

<style>
#app {
  font-family: tahoma;
  color:#282828;
  margin: 0px;
}

.product {
  display: flex;
  flex-flow: wrap;
  padding: 1rem;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px .5px 1px #d8d8d8;
}

.product-image {
  width: 80%;
}

.product-image,
.product-info {
  margin-top: 10px;
  width: 50%;
}

  .cart {
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
  }
  
  button {
    margin-top: 30px;
    border: none;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
  } 
</style>