<template>
  <div id="app">
   
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
   
  }
};
</script>

<style>

</style>
