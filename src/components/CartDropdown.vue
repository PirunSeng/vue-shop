<template>
  <div class="dropdown-clip" v-if="cart.length > 0">
    <transition name="dropdown">
      <div v-if="displayCart" class="list-group" aria-labelledby="cartDropdown">
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
</template>

<script>
import Currency from '@/components/Currency'
export default {
  props: ['cart', 'displayCart'],
  components: { Currency }
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
