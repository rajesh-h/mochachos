<template>
  <div class="container mx-auto">
    <div class="w-full max-w-xs mx-auto mt-16">
      <form class="bg-secondary shadow-md rounded px-8 pt-6 pb-8 mb-4">
        <div class="text-center uppercase text-lg p-3 mb-4">
          Signup / Welcome Back
        </div>
        <div class="mb-4">
          <label class="block text-sm font-bold my-2" for="mobilenumber">
            Mobile Number
          </label>

          <div class="flex">
            <div
              class="bg-gray-200 shadow appearance-none border border-purple-500 rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            >
              +27
            </div>
            <input
              id="mobilenumber"
              v-model="phoneNumber"
              class="bg-gray-200 shadow appearance-none border border-purple-500 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              type="text"
              placeholder="No +27 or 0 at Start"
              autocomplete="off"
            />
          </div>
        </div>
        <div class="mb-6">
          <div v-if="otpRequested" class="mb-4">
            <label class="block text-sm font-bold mb-2" for="otp">
              OTP
            </label>
            <input
              id="otp"
              v-model="otp"
              class="bg-gray-200 shadow appearance-none border border-purple-500 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              type="text"
              placeholder="*****"
              autocomplete="off"
            />
          </div>
          <div class="flex items-center justify-between">
            <button
              v-if="!otpRequested"
              class="bg-blue-500 hover:bg-blue-700 text-sm text-white uppercase py-2 px-4 mt-4 rounded focus:outline-none focus:shadow-outline"
              type="button"
              @click="verifyPhone"
            >
              Request OTP
            </button>
            <button
              v-if="otpRequested"
              class="bg-blue-500 hover:bg-blue-700 text-sm text-white uppercase py-2 px-4 mt-4 rounded focus:outline-none focus:shadow-outline"
              type="button"
              :disabled="resendOtpDisabled"
              @click="verifyPhone"
            >
              Resend OTP
            </button>
            <button
              v-if="otpRequested"
              class="bg-blue-500 hover:bg-blue-700 text-sm text-white uppercase py-2 px-4 mt-4 rounded focus:outline-none focus:shadow-outline"
              type="button"
              @click="verifyOtp"
            >
              Sign In
            </button>
          </div>
        </div>
      </form>
    </div>

    <div id="recaptcha-container"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mobilePrefix: '+27',
      phoneNumber: '',
      appVerifier: '',
      otp: '',
      otpRequested: false,
      confirmationResult: undefined,
      resendOtpDisabled: true,
    }
  },
  mounted() {
    this.initReCaptcha()
  },

  methods: {
    async verifyPhone() {
      try {
        this.confirmationResult = await this.$fireAuth.signInWithPhoneNumber(
          this.mobilePrefix + this.phoneNumber,
          this.appVerifier
        )
        // eslint-disable-next-line no-console
        console.log('response', this.confirmationResult)
        this.otpRequested = true
        setTimeout(() => (this.resendOtpDisabled = false), 30000)
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
        this.phoneNumber = ''
        this.otp = ''
        this.$router.push({ name: 'index' })
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
  },
}
</script>

<style></style>
