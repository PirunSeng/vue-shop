<template>
  <navbar :cart="cart" :cartTotal="cartTotal" :cartQty="cartQty" />
  <div class="container">
    <router-view :cart="cart" @addItem="addItem" :products="products" />
  </div>
</template>

<script>
import Navbar from '@/components/Navbar'

export default {
  data: function () {
    return {
      cart: [],
      products: []
    }
  },
  components: {
    Navbar
  },
  created() {
    fetch('https://hplussport.com/api/products/order/price')
      .then(response => response.json())
      .then(data => {
        this.products = data
      })
  },
  computed: {
    cartTotal() {
      let sum = 0
      for (let key in this.cart) {
        sum = sum + this.cart[key].product.price * this.cart[key].qty
      }
      return sum
    },
    cartQty() {
      let qty = 0
      for (let key in this.cart) {
        qty = qty + this.cart[key].qty
      }
      return qty
    }
  },
  methods: {
    addItem(product) {
      let whichProduct
      let existing = this.cart.filter((item, index) => {
        if (item.product.id == Number(product.id)) {
          whichProduct = index
          return true
        } else {
          return false
        }
      })
      if (existing.length) {
        this.cart[whichProduct].qty++
      } else {
        this.cart.push({ product, qty: 1 })
      }
    }
  }
}
</script>

<style lang="scss">
$primary: #6f42c1;
@import 'node_modules/bootstrap/scss/bootstrap';
</style>
