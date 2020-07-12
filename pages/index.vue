<template>
  <div class="container mx-auto">
    <Hero />
    <div v-if="shop.categories" class="p-2">
      <button
        v-for="cat in sortListOfArrayByKey(shop.categories)"
        :key="cat.priority"
        class="px-2 hover:text-primary hover:font-bold focus:outline-none focus:text-primary focus:font-bold focus:underline shadow-sm"
        @click="selectedCategory(cat.category)"
      >
        {{ cat.category }}
      </button>
    </div>
    <ProductList :products="getSelectedCategoryProducts" />
  </div>
</template>

<script>
export default {
  async fetch() {
    const currentShop = await this.$content('mochachos').fetch()
    this.shop = currentShop
    // eslint-disable-next-line no-console
    // console.log(this.shop)
  },
  data() {
    return {
      shop: {},
      selected_category: null,
    }
  },
  computed: {
    getSelectedCategoryProducts() {
      if (!this.selected_category) {
        return this.shop.products
      } else {
        return this.shop.products.filter((item) => {
          return item.categories.includes(this.selected_category)
        })
      }
    },
  },
  methods: {
    selectedCategory(category) {
      if (category.toLowerCase() === 'all') {
        this.selected_category = null
      } else {
        this.selected_category = category
      }
    },
    sortListOfArrayByKey(arr) {
      // Set slice() to avoid to generate an infinite loop!
      return arr.slice().sort(function (a, b) {
        return a.priority - b.priority
      })
    },
  },
}
</script>

<style></style>
