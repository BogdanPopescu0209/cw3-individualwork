<template>
  <main>
    <div class="row">
      <ul v-for="product in products" :key="product.topic">
        <div class="output">
          <figure>
            <img v-bind:src="product.image" alt="logo.png" />
          </figure>
          <p>Subject: {{ product.topic }}</p>
          <p>Location: {{ product.location }}</p>
          <p>Price: {{ product.price }}</p>
          <p>Number of spaces: {{ product.space }}</p>
          <button
            class="add"
            @click="addToCart(product)"
            v-if="canAddToCart(product)"
          >
            Add to cart
          </button>
          <button class="add" disabled="disabled" v-else>Add to cart</button>
        </div>
      </ul>
    </div>
  </main>
</template>

<script>
export default {
  name: "products",
  props: ["products"],
  data() {
    return {};
  },
  methods: {
    addToCart(product) {
      this.$emit("addProduct", product);
    },
    canAddToCart: function (product) {
      return product.space > 0;
    },
  },
};
</script>

<style scoped>
.output {
  padding-right: 10px;
  border-style: solid;
  border-color: cornflowerblue;
  border-radius: 10px;
  padding: 5px;
}

.add {
  background-color: cornflowerblue;
  color: white;
  margin-left: 100px;
  cursor: pointer;
}

img {
  height: 80px;
  width: 80px;
  float: left;
  margin-top: 50px;
}

ul {
  float: left;
}

p {
  padding-left: 120px;
}
</style>
