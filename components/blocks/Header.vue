<template>
  <header class="flex items-center justify-between bg-secondary px-4 py-3">
    <div>
      <a href="/" class="text-primary cursor font-bold uppercase">
        Mochachos
      </a>
    </div>
    <div class="flex flex-row">
      <svg
        class="h-5 w-5 fill-current cursor-pointer mx-2"
        viewBox="0 0 20 20"
        @click="toggle"
      >
        <path
          d="M10 2v16a8 8 0 1 0 0-16zm0 18a10 10 0 1 1 0-20 10 10 0 0 1 0 20z"
        />
      </svg>

      <svg
        v-if="isLoggedIn"
        class="h-5 w-5 fill-current cursor-pointer mx-2"
        viewBox="0 0 20 20"
        @click="showUserMenu = !showUserMenu"
      >
        <path
          d="M5 5a5 5 0 0 1 10 0v2A5 5 0 0 1 5 7V5zM0 16.68A19.9 19.9 0 0 1 10 14c3.64 0 7.06.97 10 2.68V20H0v-3.32z"
        />
      </svg>
      <div
        v-if="showUserMenu"
        class="origin-top-right absolute right-0 mt-8 w-56 rounded-md shadow-lg"
      >
        <div class="rounded-md bg-secondary shadow-xs">
          <div
            class="py-1"
            role="menu"
            aria-orientation="vertical"
            aria-labelledby="options-menu"
          >
            <a
              href="#"
              class="block px-4 py-2 text-sm leading-5 hover:bg-gray-100 hover:text-gray-900 focus:outline-none focus:bg-gray-100 focus:text-gray-900"
              role="menuitem"
              >Account settings</a
            >
            <a
              href="#"
              class="block px-4 py-2 text-sm leading-5 hover:bg-gray-100 hover:text-gray-900 focus:outline-none focus:bg-gray-100 focus:text-gray-900"
              role="menuitem"
              >Support</a
            >
            <a
              href="#"
              class="block px-4 py-2 text-sm leading-5 hover:bg-gray-100 hover:text-gray-900 focus:outline-none focus:bg-gray-100 focus:text-gray-900"
              role="menuitem"
              >License</a
            >

            <button
              type="submit"
              class="block w-full text-left px-4 py-2 text-sm leading-5 hover:bg-gray-100 hover:text-gray-900 focus:outline-none focus:bg-gray-100 focus:text-gray-900"
              role="menuitem"
              @click="logout()"
            >
              Sign out
            </button>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
export default {
  name: 'Header',
  components: {},
  data() {
    return {
      showUserMenu: false,
    }
  },
  computed: {
    ...mapGetters({
      isLoggedIn: 'isLoggedIn',
    }),
  },
  methods: {
    toggle() {
      this.$colorMode.preference =
        this.$colorMode.value === 'dark' ? 'light' : 'dark'
    },
    ...mapActions({
      logoff: 'signOut',
    }),
    logout() {
      this.logoff().then(() => {
        this.showUserMenu = false
        this.$router.push({ name: 'signin' })
      })
    },
  },
}
</script>

<style></style>
