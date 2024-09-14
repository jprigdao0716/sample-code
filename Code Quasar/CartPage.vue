
<template>
  <q-page padding>
    <!-- Display Cart Items -->
    <div class="cart-items-container">
      <div class="hold">
        <!-- Loop over cart items -->
        <div class="col-12 col-md" v-for="item in cartItems" :key="item.id">
          <q-card class="my-card">
            <q-img :src="item.image" class="cart-image" />
            
            <q-card-section>
              <div class="card-content">
                <div class="item-details">
                  <h2>{{ item.name }}</h2>
                  <!-- <p><b>Quantity: {{ item.quantity }}</b></p> -->
                  <!-- Align Quantity and Description horizontally -->
                  <div class="row">
                    <div class="col-4">
                      <p>Quantity: <b>{{ item.quantity }}</b></p>
                    </div>
                    <div class="col-4">
                      <p>Price: $<b>{{ item.price }}</b></p>
                  </div>
                </div>
                  
                  <div class="button-group">
                    <div class="row">
                      <div class="col-12 col-md">
                        <q-btn @click="removeFromCart(item.id)" color="negative" label="Remove" class="remove-btn" />
                      </div>
                      <div class="col-12 col-md">
                        <q-btn @click="goToCheckout" color="primary" label="Checkout" class="checkout-btn" />
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </q-card-section>
          </q-card>
        </div>
      </div>
    </div>

    <!-- Total Items Banner -->
    <q-banner class="q-mt-md total-banner">
      Total Items: {{ cartItemCount }} <br />
      Total Amount: ${{ totalAmount }}
    </q-banner>
  </q-page>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';

export default {
  computed: {
    ...mapGetters('cart', ['cartItems', 'cartItemCount', 'totalAmount']),
  },
  methods: {
    ...mapActions('cart', ['removeFromCart']),
    goToCheckout() {
      this.$router.push('/checkoutorder');
    },
  },
};
</script>

<style scoped>
.cart-items-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.my-card {
  max-width: 800px;
  margin: 10px auto;
  display: flex;
  flex-direction: row;
  align-items: center;
}

.cart-image {
  width: 280px;
  height: 200px;
  object-fit: cover;
  padding: 10px;
  border: 1px solid;
  box-shadow: 10px 5px;
  margin-left: 10px;
}

.card-content {
  font-size: 18px;
  flex-direction: row; /* Align items in a row */
  justify-content: space-between; /* Space out the content and button */
  align-items: center; /* Align items vertically */
  margin-left: 20px;
  width: 100%;
}

.card-content b{
  color: red;
}

.item-details {
  display: flex;
  flex-direction: column;
}

.button-group {
  display: flex;
  gap: 10px;
} 


.q-btn{
  border-radius: 40px;
  width: 200px;
}

.total-banner {
  background-color: #f5f5f5;
  color: #333;
  padding: 10px;
  font-size: 18px;
  font-weight: bold;
}


</style>
