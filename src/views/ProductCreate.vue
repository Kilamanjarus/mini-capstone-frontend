<script>
import router from '@/router';
import axios from 'axios';

export default {
  data: function () {
    return {
      message: "Add new Product!",
      newProduct: {},
      errors: []
    };
  },
  created: function () { },
  methods: {
    productCreate: function () {
      console.log(`Creating function...`)
      console.log(this.newProduct)
      axios.post("http://localhost:3000/products", this.newProduct)
        .then(response => {
          console.log(response.data)
          this.$router.push("/products");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  },
};
</script>
  
  <template>

  <div class="signup">
    <form v-on:submit.prevent="productCreate()">
      <h1>New Product</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{  error  }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newProduct.name" />
      </div>
      <div>
        <label>Price:</label>
        <input type="integer" v-model="newProduct.price" />
      </div>
      <div>
        <label>Description:</label>
        <input type="text" v-model="newProduct.description" />
      </div>
      <div>
        <label>Inventory:</label>
        <input type="text" v-model="newProduct.inventoryamount" />
      </div>
      <div>
        <label>Supplier Id:</label>
        <input type="text" v-model="newProduct.supplier_id" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
  
  <style>
  </style>