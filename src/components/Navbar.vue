<template>
  <!-- <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/checkout">Checkout</router-link>
  </div> -->
  <nav class="navbar navbar-light sticky-top pr-3">
    <div class="container-fluid">
      <div
        v-if="cart.length"
        class="w-100 navbar-text ml-auto d-flex justify-content-end position-relative"
      >
        <div
          class="mr-auto d-flex align-items-end flex-column bd-highlight mb-3 position-absolute"
        >
          <div class="mb-2">
            <span class="font-weight-bold bg-white">
              <currency :amt="cartTotal"></currency>
            </span>
            <button
              @click="displayCart = !displayCart"
              class="btn btn-sm btn-success ml-3"
              id="cartDropdown"
              aria-haspopup="true"
              aria-expanded="false"
            >
              <fa icon="shopping-cart" />
              {{ cart.length }}
            </button>
          </div>
          <div class="dropdown-clip">
            <transition name="dropdown">
              <div
                v-if="displayCart"
                class="list-group"
                aria-labelledby="cartDropdown"
              >
                <div
                  v-for="(item, index) in cart"
                  :key="index"
                  class="list-group-item d-flex justify-content-between"
                >
                  <div>{{ item.name }}</div>
                  <div class="ml-3 font-weight-bold">
                    <currency :amt="item.price"></currency>
                  </div>
                </div>
              </div>
            </transition>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import Currency from './Currency.vue'
export default {
  props: ['cart'],
  data: function () {
    return { displayCart: false }
  },
  components: { Currency },
  computed: {
    cartTotal() {
      return this.cart.reduce((inc, item) => Number(item.price) + inc, 0)
    }
  }
}
</script>

<style>
.dropdown-clip {
  overflow: hidden;
}
.dropdown-enter-active,
.dropdown-leave-active {
  transition: all 0.5s ease-in-out;
  transform: auto;
}
.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateY(-300px);
}
</style>
