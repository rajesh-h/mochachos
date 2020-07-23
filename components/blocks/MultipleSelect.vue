<template>
  <span>
    <label v-for="choice in option.choices" :key="choice" class="">
      <input
        v-model="selectedChoices"
        :value="choice"
        type="checkbox"
        class="form-checkbox ml-2"
        :disabled="
          selectedChoices.length >= option.max &&
          selectedChoices.indexOf(choice) === -1
        "
        @change="updateSelectedOptionMulti"
      /><span class="ml-2">{{ choice }}</span>
    </label>
  </span>
</template>

<script>
export default {
  props: {
    option: {
      type: Object,
      default() {
        return { selected: [] }
      },
    },
  },
  data() {
    return {
      selectedChoices: this.option.selected,
    }
  },
  methods: {
    updateSelectedOptionMulti() {
      /* This is slightly complex logic
      MultipleSelect is Grand Child to Product
      OtherOptions is Child to Product
      Here we emit name and selected choices so on product we use these to update the specific option like toppings
      On Child component i.e. OtherOptions.vue we use v-on="$listeners" so it passes the events
      */

      this.$emit('onUpdateSelectedMulti', {
        name: this.option.name,
        selected: this.selectedChoices,
      })
    },
  },
}
</script>

<style></style>
