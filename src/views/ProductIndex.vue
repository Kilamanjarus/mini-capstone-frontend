<script>
import axios from 'axios';

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      products: {}
    };
  },
  created: function () {
    this.productsIndex();
  },
  methods: {
    productsIndex: function () {
      console.log(`Getting products....`)
      axios.get(`http://localhost:3000/products.json`).then(response => {
        console.log(response.data)
        this.products = response.data
      })
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>Products</h1>
    <p v-for="product in products">
      <a v-bind:href="`/products/${product.id}`">{{  product.name  }}</a>
      {{  product.price  }}
    </p>
  </div>
</template>

<style>
</style>