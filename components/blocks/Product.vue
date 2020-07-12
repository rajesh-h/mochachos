<template>
  <div>
    <div class="flex bg-secondary rounded-lg items-stretch p-3">
      <img class="h-24 w-24 rounded-lg self-center" :src="product.img" />

      <div class="relative flex-1 text-left ml-2">
        <h2 class="text-lg self-start">{{ product.name }}</h2>

        <div v-if="product.description" class="text-xs">
          {{ product.description }}
        </div>
        <div class="absolute inset-x-0 bottom-0">
          <div class="flex flex-row float-right">
            <svg
              class="h-5 w-5 fill-current text-primary cursor-pointer hover:text-default"
              viewBox="0 0 20 20"
            >
              <path
                d="M10 20a10 10 0 1 1 0-20 10 10 0 0 1 0 20zm0-2a8 8 0 1 0 0-16 8 8 0 0 0 0 16zm5-9v2H5V9h10z"
              />
            </svg>
            <div class="mx-1 px-2">4</div>
            <svg
              class="h-5 w-5 fill-current text-primary cursor-pointer hover:text-default"
              viewBox="0 0 20 20"
              @click="showModal = true"
            >
              <path
                d="M11 9h4v2h-4v4H9v-4H5V9h4V5h2v4zm-1 11a10 10 0 1 1 0-20 10 10 0 0 1 0 20zm0-2a8 8 0 1 0 0-16 8 8 0 0 0 0 16z"
              />
            </svg>
          </div>
        </div>
      </div>
    </div>
    <div>
      <modal :showing="showModal" @close="showModal = false">
        <div>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Incidunt
          tenetur autem dignissimos dolore earum odio asperiores, maxime quas
          saepe accusamus a deleniti qui nam ipsa error quod, suscipit est
          ullam? Lorem ipsum dolor sit amet consectetur adipisicing elit. Ex
          cupiditate consequatur esse quae vero alias temporibus consectetur,
          eius beatae quisquam voluptas obcaecati odio iure saepe magnam ad eos
          fuga aperiam! Lorem ipsum dolor sit amet, consectetur adipisicing
          elit. Dignissimos esse est eveniet accusantium delectus cumque, quidem
          dicta architecto ad quas necessitatibus, soluta repudiandae
          repellendus quam ipsa voluptas dolor amet ex.
        </div>
      </modal>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Product',
  props: {
    product: {
      type: Object,
      default() {
        return {
          categories: ['Lunch'],
          price: '27',
          options: [
            {
              toppings: {
                max: 3,
                selection: 'multi',
                choices: ['Onion', 'Chilli', 'Pineaple', 'Chicken', 'Prawns'],
              },
            },
            {
              size: {
                choices: ['2L', '500 ML', '1L'],
                selection: 'single',
                max: 1,
              },
            },
          ],
          description:
            'Grilled chicken breast, tomato, rocca, guacamole, herb aioli sauce. .',
          name: 'The Grilled',
          _id: 1,
          img:
            'https://storage.googleapis.com/testbeta-2020.appspot.com/mochachos/thegrilled?alt=media',
        }
      },
    },
  },
  data() {
    return {
      showModal: false,
    }
  },
  method: {},
}
</script>

<style></style>
