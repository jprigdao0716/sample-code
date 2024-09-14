<template>
  <q-page padding>
    <q-card class="my-card">
      <div v-if="addToCartMessage" class="add-to-cart-message" style="background-color: bisque; padding: 15px;">
            {{ addToCartMessage }}<br>

            <q-btn flat to="/cart" class="cart-btn">
             <b>View Cart</b>
      
      </q-btn>

          </div>
      <q-img :src="product.image" />
      <q-card-section>
        <div class="product-details">
          <h2>{{ product.name }}</h2>
          <p style="color: red">${{ product.price }}.00</p>
          <p>{{ product.description }}</p>
          <div class="quantity-section">
            <q-input
              v-model="quantity"
              type="number"
              min="1"
              outlined
              class="quantity-input"
            />
          </div>
          <div class="container">
  <div class="row button-group">
    <div class="col-12 col-sm-6 mb-2">
      <q-btn
        @click="addToCart"
        color="primary"
        label="Add to Cart"
        class="add-to-cart-btn w-100"
      />
    </div>
    <div class="col-12 col-sm-6 mb-2">
      <q-btn
        @click="goToCheckout"
        color="secondary"
        label="Checkout"
        class="checkout-btn w-100"
      />
    </div>
  </div>
</div>
</div>


        <!-- Tabs -->
        <q-tabs v-model="tab" class="product-tabs">
          <q-tab name="description" label="Description" />
          <q-tab name="reviews" label="Reviews" />
        </q-tabs>

        <q-tab-panels v-model="tab" animated>
          <q-tab-panel name="description">
            <h2>Description</h2>
            <p>{{ product.description }}</p>
          </q-tab-panel>
          <q-tab-panel name="reviews">
            <h2>Reviews</h2>
            <p>{{ product.reviews }}</p>
          </q-tab-panel>
        </q-tab-panels>
      </q-card-section>
    </q-card>

<!-- Related Products Section -->
<q-card class="related-products-card bg-transparent">
  <q-card-section>
    <h3>Related Products</h3>
    <div class="related-products">
      <div class="product-grid">
        <div
          v-for="relatedProduct in relatedProducts"
          :key="relatedProduct.id"
          class="product-card"
        >
          <q-img :src="relatedProduct.image" class="img-fluid mb-2" />
          <p>{{ relatedProduct.name }}</p>
          <q-btn
            @click="viewProduct(relatedProduct.id)"
            color="primary"
            label="View Details"
            class="related-btn w-100 mt-2"
          />
        </div>
      </div>
    </div>
  </q-card-section>
</q-card>

  </q-page>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  data() {
    return {
      product: {
        id: 1,
        name: 'JACKSON FLYING V',
        description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit.',
        image: 'src/assets/eg1.jpg',
        reviews: 'No reviews yet.',
      },
      relatedProducts: [
        { id: 2, name: 'ESP LTD ARROW', image: 'src/assets/eg2.jpg' },
        { id: 3, name: 'GIBSON FLYING V', image: 'src/assets/eg3.jpg' },
      ],
      quantity: 1,
      tab: 'description',
      addToCartMessage: '', // Message to display after adding to cart
    };
  },
  
  async created() {
    const productId = this.$route.params.id;
    // Fetch product details based on productId
    await this.fetchProductDetails(productId);
  },
  methods: {
    ...mapActions('cart', ['addToCart']),
    async fetchProductDetails(productId) {
      // Fetch product details from your API or store
      const products = [
        { id: 1, name: 'JACKSON FLYING V', price: 300.00, description: ' Lorem ipsum dolor sit amet consectetur adipisicing elit. Sed facilis voluptas autem consequatur dolorem quod amet, debitis praesentium expedita placeat ipsum, esse magni hic labore iste! Vel hic cupiditate dolorem.', image: 'src/assets/eg1.jpg', reviews: 'No reviews yet.' },
        { id: 2, name: 'JACKSON FLYING V WHITE', price: 300.00, description: ' Lorem ipsum dolor sit amet consectetur adipisicing elit. Sed facilis voluptas autem consequatur dolorem quod amet, debitis praesentium expedita placeat ipsum, esse magni hic labore iste! Vel hic cupiditate dolorem.', image: 'src/assets/eg2.jpg', reviews: 'Good product.' },
        { id: 3, name: 'JACKSON FLYING FLOYD ROSE', price: 280.00, description: ' Lorem ipsum dolor sit amet consectetur adipisicing elit. Sed facilis voluptas autem consequatur dolorem quod amet, debitis praesentium expedita placeat ipsum, esse magni hic labore iste! Vel hic cupiditate dolorem.', image: 'src/assets/eg3.jpg', reviews: 'Good product.' },
        { id: 4, name: 'ESP LTD ARROW', price: 330.00, description: ' Lorem ipsum dolor sit amet consectetur adipisicing elit. Sed facilis voluptas autem consequatur dolorem quod amet, debitis praesentium expedita placeat ipsum, esse magni hic labore iste! Vel hic cupiditate dolorem.', image: 'src/assets/LARROW200BLK.jpg', reviews: 'Good product.' },
        { id: 5, name: 'GIBSON FLYING V', price: 280.00, description: ' Lorem ipsum dolor sit amet consectetur adipisicing elit. Sed facilis voluptas autem consequatur dolorem quod amet, debitis praesentium expedita placeat ipsum, esse magni hic labore iste! Vel hic cupiditate dolorem.', image: 'src/assets/eg6.jpg', reviews: 'Good product.' },
        { id: 6, name: 'JACKSON EXPLORER', price: 340.00, description: ' Lorem ipsum dolor sit amet consectetur adipisicing elit. Sed facilis voluptas autem consequatur dolorem quod amet, debitis praesentium expedita placeat ipsum, esse magni hic labore iste! Vel hic cupiditate dolorem.', image: 'src/assets/eg7.jpg', reviews: 'Good product.' },
        // Add more products as needed
      ];
      this.product = products.find(p => p.id === parseInt(productId));
    },
    addToCart() {
      if (this.product) {
        const productToAdd = { ...this.product, quantity: this.quantity };
        console.log('Adding to Cart:', productToAdd);
        this.$store.dispatch('cart/addToCart', productToAdd);
        this.addToCartMessage = 'Product has been added to cart'; // Set the message
      }
    },
    goToCheckout() {
    this.$router.push({
      path: '/checkoutorder',
      query: {
        id: this.product.id,
        name: this.product.name,
        price: this.product.price,
        quantity: this.quantity
      }
      
    });
    
},
viewProduct(id) {
    this.$router.push(`/product/${id}`);
  },
},
} 
</script>

<style scoped>

.q-page {
    background-color: aliceblue;
    /* background: url(/src/assets/lespaul.jpg) no-repeat center center fixed; */
    background-size: cover;
    /* display: flex; */
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}

.my-card {
  max-width: 600px;
  margin: auto;
}

.product-details {
  margin-bottom: 20px;
}

.mb-4, .related-btn{
  margin: 50px;
}

.quantity-section {
  display: flex;
  align-items: center;
  margin-top: 50px;
}

.quantity-input {
  max-width: 500px;
  margin-left: 0rem;
  height: 100px;
}

.button-group {
  display: flex;
  gap: 0px;
  margin: 0px;

}

.product-tabs {
  margin-top: 20px;
}

.related-products-card {
  margin-top: 40px;
  margin: 15px;
}

.related-products {
  display: flex;
  gap: 70px;
  justify-content: space-evenly;
}


.related-products .container{
  display: flex;
}

.products-holder{
  margin: 30px;
}

.add-to-cart-btn,
.checkout-btn {
  width: 200px;
}

.related-btn {
  width: 230px;
  margin: auto;
}

.add-to-cart-message {
  color: green;
  margin-top: 10px;
}

.product-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 15px; /* Space between items */
}

.product-card {
  flex: 1 1 calc(33.333% - 30px); /* 3 items per row with space between */
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.product-card img {
  max-width: 100%;
  height: auto;
}

.related-btn {
  max-width: 200px; /* Adjust as needed */
}

/* Responsive styles */
@media (max-width: 1024px) {
  .product-card {
    flex: 1 1 calc(50% - 30px); /* 2 items per row */
  }
}

@media (max-width: 768px) {
  .product-card {
    flex: 1 1 100%; /* 1 item per row */
  }
}

</style>
