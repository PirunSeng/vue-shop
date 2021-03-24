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
  props: ['products'],
  data: function () {
    return {
      max: 50,
      cart: []
    }
  },

  computed: {
    filteredProducts() {
      return this.products.filter(item => item.price < Number(this.max))
    }
  }
}
</script>
