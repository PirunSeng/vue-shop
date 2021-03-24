<template>
  <section class="container">
    <range-selector :filteredProducts="filteredProducts" v-model="max" />
    <product-list :filteredProducts="filteredProducts" />
  </section>
</template>

<script>
import ProductList from '@/components/ProductList'
import RangeSelector from '@/components/RangeSelector'

export default {
  components: { ProductList, RangeSelector },
  name: 'Home',
  data: function () {
    return {
      max: 50,
      cart: [],
      displayCart: false,
      products: []
    }
  },
  created() {
    fetch('https://hplussport.com/api/products/order/price')
      .then(response => response.json())
      .then(data => {
        this.products = data
      })
  },
  computed: {
    filteredProducts() {
      return this.products.filter(item => item.price < Number(this.max))
    }
  }
}
</script>
