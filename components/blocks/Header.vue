<template>
  <header class="flex items-center justify-between bg-secondary px-4 py-3">
    <div>
      <a href="/" class="text-primary cursor font-bold uppercase">
        Mochachos
      </a>
    </div>
    <div>
      <svg
        class="h-5 w-5 fill-current cursor-pointer"
        viewBox="0 0 20 20"
        @click="toggle"
      >
        <path
          d="M10 2v16a8 8 0 1 0 0-16zm0 18a10 10 0 1 1 0-20 10 10 0 0 1 0 20z"
        />
      </svg>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
  methods: {
    toggle() {
      this.$colorMode.preference =
        this.$colorMode.value === 'dark' ? 'light' : 'dark'
    },
  },
}
</script>

<style></style>
