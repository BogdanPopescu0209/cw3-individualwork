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
          <div v-if="showProduct">
            <products @addProduct="addToCart" :products="products"></products>
          </div>

          <div v-else>
            <checkout @deleteProduct="deleteFromCart" :cart="cart"></checkout>
          </div>
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

  methods: {
    addToCart(product) {
      this.cart.push({
        _id: product._id,
        topic: product.topic,
        location: product.location,
        price: product.price,
        quantity: product.space,
        image: product.image,
      });

      for (let i = 0; i < this.products.length; i++) {
        if (product.topic === this.products[i].topic) {
          let newSpace = this.products[i].space - 1;
          this.products[i].space = newSpace;
        }
      }
    },
    deleteFromCart(product) {
      for (let i = 0; i < this.cart.length; i++) {
        if (this.cart[i].topic === product.topic) {
          this.cart.splice(i, 1);

          product.quantity++;

          if (this.cart.length === 0) {
            this.showProduct = true;
          }
          break;
        }
      }

      for (let i = 0; i < this.products.length; i++) {
        if (product.topic === this.products[i].topic) {
          let newSpace = this.products[i].space + 1;
          this.products[i].space = newSpace;
        }
      }
    },
    showCheckout() {
      this.showProduct = this.showProduct ? false : true;
    },
  },
  
  watch: {
    searchItem: async function () {
      if (this.searchItem.length > 0) {
        let t = this;
        await fetch(
          "https://lessons-online-store.herokuapp.com/search/lessons/" +
            this.searchItem
        ).then(function (response) {
          response.json().then(function (json) {
            t.products = json;
          });
        });
      } else {
        let t = this;
        fetch(
          "https://lessons-online-store.herokuapp.com/collection/lessons"
        ).then(function (response) {
          response.json().then(function (json) {
            t.products = json;
          });
        });
      }
    },
  },
};
</script>

<style>
</style>
