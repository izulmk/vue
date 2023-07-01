<template>
  <div>
    <h1>IDShop</h1>
    <navbar :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal" @toggle-slide="toggleSlider" @delete-item="deleteItem"></navbar>
    <price-slider :sliderStatus="sliderStatus" v-model:maximum="maximum"></price-slider>
    <pre>
            <!-- <div>{{ JSON.stringify(products, null, 2) }}</div> -->
        </pre>
    <product-list :products="products" :maximum="maximum" @add-item="addItem"></product-list>
  </div>
</template>

<script>
import Navbar from "./Navbar.vue";
import PriceSlider from "./PriceSlider.vue";
import ProductList from "./ProductList.vue";

export default {
  name: "ProductsView",
  props: ["products", "maximum", "cart", "cartQty", "cartTotal", "sliderStatus", "sliderState"],
  components: {
    Navbar,
    PriceSlider,
    ProductList,
  },
  methods: {
    toggleSlider: function () {
      this.$emit("toggle");
    },
    addItem: function () {
      this.$emit("add", item);
    },
    deleteItem: function (index) {
      this.$emit("delete", index);
    },
  },
};
</script>
