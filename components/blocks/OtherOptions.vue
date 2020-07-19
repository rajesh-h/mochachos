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
                :value="choice"
                :name="option.name"
                type="radio"
                class="form-radio ml-2"
                @change="updateSelectedOptionSingle()"
              /><span class="ml-2">{{ choice }}</span>
            </label>
          </div>
          <div v-if="option.selection === 'multi'" class="p-2">
            <span>( max {{ option.max }} )</span>
            <label v-for="choice in option.choices" :key="choice" class="">
              <input
                :v-model="option.selected"
                :value="choice"
                :name="option.name"
                type="checkbox"
                class="form-checkbox ml-2"
                :disabled="1 !== 1"
                @change="updateSelectedOptionMulti()"
              /><span class="ml-2">{{ choice }}</span>
            </label>
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
    updateSelectedOptionSingle() {
      // eslint-disable-next-line no-console
      // console.log(choice)
      // eslint-disable-next-line no-console
      // console.log(this.$refs)
      this.$emit('onUpdateSelectedSingle', event)
    },

    updateSelectedOptionMulti() {
      // eslint-disable-next-line no-console
      console.log(this.otherOptions[0])
      // eslint-disable-next-line no-console
      // console.log(this.$refs)
      this.$emit('onUpdateSelectedMulti', event)
    },
  },
}
</script>

<style></style>
