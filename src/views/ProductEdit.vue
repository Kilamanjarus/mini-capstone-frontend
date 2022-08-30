<script>
import axios from 'axios';

export default {
  data: function () {
    return {
      message: "Welcome to About Page!",
      currentProduct: {}
    };
  },
  created: function () {
    this.productShow();
  },
  methods: {
    productShow: function (product) {
      console.log(`Showing product...`)
      console.log(this.$route.params.id)
      axios.get(`http://localhost:3000/products/${this.$route.params.id}.json`).then(response => {
        console.log(response.data)
        this.currentProduct = response.data
      })
    },
    updateProduct: function () {
      console.log(`Editing product...`)
      axios.patch(`http://localhost:3000/products/${this.$route.params.id}.json`, this.currentProduct).then(response => {
        console.log(response.data)
        this.$router.push(`/products`);
      })
    },
    deleteProduct: function () {
      console.log(`Deleting product...`)
      axios.delete(`http://localhost:3000/products/${this.$route.params.id}.json`).then(response => {
        console.log(response.data)
        this.$router.push(`/products`);
      })
    }
  },
};
</script>
  
  <template>
  <p><b>{{  currentProduct.name  }}</b></p>
  <p><button @click="deleteProduct()">Delete!</button></p>
  {{  currentProduct  }}
  <div>Name: <input type="text" v-model="this.currentProduct.name"></div>
  <div>Price: <input type="text" v-model="this.currentProduct.price"></div>
  <div>Description: <input type="text" v-model="this.currentProduct.description"></div>
  <div>Supplier ID: <input type="text" v-model="this.currentProduct.supplier.id"></div>
  <div>Inventory Amount: <input type="text" v-model="this.currentProduct.inventoryamount"></div>
  <button @click="updateProduct()">Update Product!</button>
</template>
  
  <style>
  </style>