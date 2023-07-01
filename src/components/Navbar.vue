<template>
  <nav class="navbar navbar-light fixed-top">
    <div class="navbar-text ml-auto d-flex">
      <button class="btn btn-sm btn-outline-success" @click="$parent.$emit('toggle-slide')">
        <font-awesome-icon icon="dollar-sign" />
      </button>
      <div class="dropdown ml-2" v-if="cart.length > 0">
        <button class="btn btn-success btn-sm dropdown-toggle" id="dropdownCart" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          <span class="badge badge-pill badge-light">{{ cartQty }}</span>
          <i class="fas fa-shopping-cart mx-2"></i>
          <font-awesome-icon icon="shopping-cart" />
          <price :value="Number(cartTotal)" />
        </button>
        <div class="dropdown-menu dropdown-menu-right" aria-labelledby="dropdownCart">
          <div v-for="(item, index) in cart" :key="index">
            <div class="dropdown-item-text text-nowrap text-right">
              <span class="badge badge-pill badge-warning align-text-top mr-1">
                {{ item.qty }}
              </span>
              {{ item.product.name }}
              <b>{{ calculateTotal(item.qty, item.product.price) }}</b>
              <a href="#" class="badge badge-danger text-white" @click.stop="$emit('delete-item', index)"> - </a>
            </div>
          </div>
          <router-link class="btn btn-sm btn-outline-info text-dark float-right mr-2" to="/checkout"> Checkout </router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import Price from "./Price.vue";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  name: "NavbarTag",
  props: ["cart", "cartQty", "cartTotal"],
  components: {
    Price,
    FontAwesomeIcon,
  },
  methods: {
    calculateTotal(qty, price) {
      return "Rp" + (qty * price).toFixed(2);
    },
  },
};
</script>
