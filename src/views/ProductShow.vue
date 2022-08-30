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
    }
  },
};
</script>
  
  <template>
  <div class="home">
    <h1>{{  currentProduct  }}</h1>
  </div>
</template>
  
  <style>
  </style>