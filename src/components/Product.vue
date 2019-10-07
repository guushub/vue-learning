<template>
 <div class="product">
      <div class="product-image">
        <img :src="image" />
      </div>

      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inventory > 10">In Stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Almost out!</p>
        <p v-else>Out of Stock</p>
        <p>Shipping: {{ shipping() }}</p>
        <ul>
          <li v-for="detail in details" :key="detail">{{ detail }}</li>
        </ul>

        <div v-for="variant in variants" 
              :key="variant.variantId"
              class="color-box"
              :style="{ backgroundColor: variant.variantColor }"
              @mouseover="updateImage(variant.variantImage)">
        </div>

        <button v-on:click="addToCart" 
                :disabled="!inStock"
                :class="{ disabledButton: !inStock }">Add to Cart</button>

        <div class="cart" ><p>Cart ({{ cart }})</p></div>
      </div>
    </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';

@Component
export default class Product extends Vue {
  private product: string = 'Socks';
  private image = '';
  private inventory: number = 10;
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
  public get inStock(): boolean {
    return this.inventory > this.cart;
  }
  @Prop() private premium!: boolean;
  constructor() {
    super();
    this.image = this.variants[0].variantImage;
  }

  private addToCart(): void {
    this.cart += 1;
  }

  private updateImage(img: string) {
    this.image = img;
  }

  private shipping() {
      if (this.premium) {
          return 'Free';
      }
      return '2.99';
  }
}

interface ProductVariant {
  variantId: number;
  variantColor: string;
  variantImage: string;
}
</script>

<style>

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

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
}

.disabledButton {
  background-color: #d8d8d8;
}
</style>