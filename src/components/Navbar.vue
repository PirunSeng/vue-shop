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
              @click="toggleCartMenu"
              class="btn btn-sm btn-success ml-3"
              id="cartDropdown"
              aria-haspopup="true"
              aria-expanded="false"
            >
              <fa icon="shopping-cart" />
              {{ cart.length }}
            </button>
          </div>
          <cart-dropdown :cart="cart" :displayCart="displayCart" />
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import CartDropdown from '@/components/CartDropdown'
import Currency from '@/components/Currency'
export default {
  props: ['cart'],
  data: function () {
    return { displayCart: false }
  },
  components: { Currency, CartDropdown },
  computed: {
    cartTotal() {
      return this.cart.reduce((inc, item) => Number(item.price) + inc, 0)
    }
  },
  methods: {
    toggleCartMenu() {
      this.displayCart = !this.displayCart
    }
  }
}
</script>
