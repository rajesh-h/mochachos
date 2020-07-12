<template>
  <div class="flex flex-wrap">
    <div
      v-for="product in products"
      :key="product._id"
      class="p-2 w-full sm:w-1/2 lg:w-1/3"
    >
      <Product :product="product" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductList',
  props: {
    products: {
      type: Array,
      default() {
        return []
      },
    },
  },
}
</script>

<style></style>
