<template>
  <div class="container mx-auto">
    <div>
      <div v-if="!user">
        Please login
      </div>
      <div v-else class="mt-4">
        <ProductList :products="items" />
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
export default {
  // async fetch() {
  //   if (!this.$store.state.authUser) {
  //     // When no user send to signin page
  //     this.$router.push({ name: 'signin' })
  //   }
  // else {
  //   // eslint-disable-next-line no-console
  //   // console.log(this.$store.state.authUser)
  //   const currentShop = await this.$content('mochachos').fetch()
  //   this.shop = currentShop
  // }
  // },
  computed: {
    user() {
      // eslint-disable-next-line no-console
      console.log(this.$store.state.authUser)
      return (this.$store.state.authUser || {}).uid || null
    },
    ...mapGetters({
      items: 'cart/getItems',
      checkCart: 'cart/checkCart',
      getQty: 'cart/getQty',
    }),
  },
  methods: {
    ...mapActions({
      addToCart_vx: 'cart/addToCart',
      addAdditinalInfo: 'cart/addAdditionalDetails',
    }),
  },
}
</script>

<style></style>
