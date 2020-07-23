<template>
  <div>
    <fieldset class="p-2 m-2 bg-primary rounded-md border border-purple-500">
      <legend class="text-sm">Options</legend>
      <div class="flex flex-col">
        <div
          v-for="option in otherOptions"
          :key="option.name"
          class="flex flex-row text-xs"
        >
          <div class="uppercase p-2">{{ option.name }} :</div>

          <div v-if="option.selection === 'single'" class="p-2">
            <label v-for="choice in option.choices" :key="choice" class="">
              <input
                :id="choice"
                v-model="option.selected"
                :name="option.name"
                :value="choice"
                type="radio"
                class="form-radio ml-2"
                @change="updateSelectedOptionSingle(option.name, choice)"
              /><span class="ml-2">{{ choice }}</span>
            </label>
          </div>
          <div v-if="option.selection === 'multi'" class="p-2">
            <span>( max {{ option.max }} )</span>

            <MultipleSelect :option="option" v-on="$listeners" />
          </div>
        </div>
      </div>
    </fieldset>
  </div>
</template>

<script>
export default {
  props: {
    otherOptions: {
      type: Array,
      default() {
        return [
          {
            toppings: {
              max: 3,
              selection: 'multi',
              choices: ['Onion', 'Chilli', 'Pineaple', 'Chicken', 'Prawns'],
              selected: [],
            },
          },
          {
            color: {
              choices: ['RED', 'Gray', 'Blue'],
              selection: 'single',
              max: 1,
              selected: '',
            },
          },
        ]
      },
    },
  },
  methods: {
    updateSelectedOptionSingle(name, value) {
      /* Since this is single choice we deal this slightly different to multiple select
      We pass in the whole event so we get the name and value through the event which can be used in Product.vue */
      this.$emit('onUpdateSelectedSingle', { name, selected: value })
    },
  },
}
</script>

<style></style>
