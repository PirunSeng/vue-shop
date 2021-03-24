<template>
  <label for="max-price" class="form-label h2"
    >Max price (${{ modelValue }})</label
  >
  <div class="badge bg-success ml-3">
    results: {{ filteredProducts.length }}
  </div>
  <input
    v-model.number="max"
    type="range"
    class="form-range"
    min="0"
    max="130"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>

<script>
export default {
  props: ['filteredProducts', 'modelValue']
}
</script>

<style></style>
