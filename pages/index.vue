/* eslint-disable no-console */ /* eslint-disable no-console */
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
  name: 'Home',
  components: {},
  async fetch() {
    if (!this.$store.state.authUser) {
      // When no user send to signin page
      this.$router.push({ name: 'signin' })
    } else {
      // eslint-disable-next-line no-console
      console.log(this.$store.state.authUser)
      const currentShop = await this.$content('mochachos').fetch()
      this.shop = currentShop
    }
  },
  data() {
    return {
      shop: {},
      selected_category: null,
      phoneNumber: '',
      appVerifier: '',
      otp: '',
      confirmationResult: undefined,
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
  async verifyPhone() {
    try {
      this.confirmationResult = await this.$fireAuth.signInWithPhoneNumber(
        this.phoneNumber,
        this.appVerifier
      )
      // eslint-disable-next-line no-console
      console.log('response', this.confirmationResult)
    } catch (e) {
      // eslint-disable-next-line no-console
      console.log('error', e)
    }
  },
  async verifyOtp() {
    try {
      const result = await this.confirmationResult.confirm(this.otp)
      // eslint-disable-next-line no-console
      console.log('result', result)
    } catch (error) {
      // eslint-disable-next-line no-console
      console.log('error', error)
    }
  },
  initReCaptcha() {
    setTimeout(() => {
      const appVerifier = new this.$fireAuthObj.RecaptchaVerifier(
        'recaptcha-container',
        {
          size: 'invisible',
          callback(response) {
            // eslint-disable-next-line no-console
            console.log('response', response)
          },
          'expired-callback'() {
            // eslint-disable-next-line no-console
            console.log('expired-callback')
          },
        }
      )
      this.appVerifier = appVerifier
    }, 1000)
  },
}
</script>

<style></style>
