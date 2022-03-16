<template>
  <div id="app">
    <div class="container-fluid">
      <div class="container-fluid">
        <div class="row">
          <div class="col-lg"></div>

          <div class="col-lg">
            <header>
              <h1>{{ sitename }}</h1>

              <div class="row">
                <button
                  v-if="cart.length > 0"
                  class="checkout"
                  v-on:click="showCheckout"
                >
                  {{ cart.length }}
                  <span class="fas fa-cart-plus"></span> Checkout
                </button>
              </div>
              <input
                class="search"
                type="text"
                v-model="searchItem"
                placeholder="Search..."
              />

              <button class="searchBtn">
                <span class="fas fa-search"></span>Search
              </button>
            </header>
          </div>

          <div class="col-lg"></div>
        </div>

        <br />

        <div class="row">
          
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import products from "./components/porducts.vue";
import checkout from "./components/checkout.vue";

export default {
  name: "App",
  components: { products, checkout },
  data() {
    return {
      sitename: "After School Club",
      cart: [],
      products: [],
      showProduct: true,
      searchItem: "",
    };
  },

  methods: {},
};
</script>

<style>
</style>
