<template>
  <div>
    <div class="row">
      <ul v-for="product in cart" :key="product.topic">
        <div class="output">
          <img v-bind:src="product.image" alt="logo.png" />
          <p>Subject: {{ product.title }}</p>
          <p>Location: {{ product.location }}</p>
          <p>Price: {{ product.price }}</p>
          <p>Number of spaces: 1</p>
          <button class="add" @click="deleteFromCart(product)">
            <span class="fas fa-trash"></span> Delete
          </button>
        </div>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Form",
  props: ["cart"],
  data() {
    return {};
  },
  methods: {
    deleteFromCart: function (product) {
      this.$emit("deleteProduct", product);
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