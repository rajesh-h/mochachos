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
          <span class="ml-4">R {{ product.price }}</span>
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
              @click="addToCart"
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
      <modal
        :showing="showModal"
        :options="modalOptions"
        @close="showModal = false"
      >
        <div>
          <table class="table-fixed w-full">
            <thead>
              <tr>
                <th class="w-1/2 px-2 py-2">Title</th>
                <th class="w-1/6 px-2 py-2">Quantity</th>
                <th class="w-1/6 px-2 py-2">Price</th>
                <th class="w-1/6 px-2 py-2"></th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td class="px-2 py-2 text-sm md:text-md">{{ product.name }}</td>
                <td class="px-2 py-2 text-sm md:text-md">
                  <div class="flex flex-row justify-around items-center">
                    <button
                      class="text-md md:text-2xl text-red-600 p-2 font-bold focus:outline-none"
                    >
                      -
                    </button>
                    <div class="self-center font-semibold">
                      0
                    </div>
                    <button
                      class="text-md md:text-2xl text-primary p-2 font-bold focus:outline-none"
                    >
                      +
                    </button>
                  </div>
                </td>
                <td class="px-2 py-2 text-center text-sm md:text-md">
                  {{ product.price }}
                </td>
                <td
                  class="self-center px-2 py-2 text-center text-md md:text-xl text-red-600"
                >
                  <button
                    class="text-md md:text-xl text-red-600 p-2 font-bold focus:outline-none"
                  >
                    x
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
          <OtherOptions
            :other-options="product.otherOptions"
            @onUpdateSelectedSingle="updateSelectedSingle"
            @onUpdateSelectedMulti="updateSelectedMulti"
          />
          <textarea
            id=""
            class="p-2 m-2 bg-primary rounded-md border border-purple-500"
            name=""
            cols="30"
            rows="2"
            placeholder="Special Instructions"
          ></textarea>
        </div>
        <button @click="printProduct()">Add</button>
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
        return {}
        // return {
        //   categories: ['Lunch'],
        //   price: '27',
        //   hasOptions: true,
        //   canInstruct: true,
        //   options: [
        //     {
        //       toppings: {
        //         max: 3,
        //         selection: 'multi',
        //         choices: ['Onion', 'Chilli', 'Pineaple', 'Chicken', 'Prawns'],
        //       },
        //     },
        //     {
        //       size: {
        //         choices: ['2L', '500 ML', '1L'],
        //         selection: 'single',
        //         max: 1,
        //       },
        //     },
        //   ],
        //   description:
        //     'Grilled chicken breast, tomato, rocca, guacamole, herb aioli sauce. .',
        //   name: 'The Grilled',
        //   _id: 1,
        //   img:
        //     'https://storage.googleapis.com/testbeta-2020.appspot.com/mochachos/thegrilled?alt=media',
        // }
      },
    },
  },
  data() {
    return {
      showModal: false,
      modalOptions: {
        // modal: 'max-h-90',
      },
      orderPerProduct: [],
    }
  },
  methods: {
    addToCart() {
      if (
        this.product.hasOptions ||
        this.product.canInstruct ||
        this.product.hasPriceOptions
      ) {
        // eslint-disable-next-line no-console
        console.log('Option to be selected')
        this.showModal = true
      } else {
        // eslint-disable-next-line no-console
        console.log('No Option can be selected, so adding directly')
      }
    },
    printProduct(prod) {
      // eslint-disable-next-line no-console
      console.log(this.product)
    },

    updateSelectedSingle(event) {
      // eslint-disable-next-line no-console
      console.log(event)
      this.product.otherOptions.forEach((elem) => {
        // eslint-disable-next-line no-console
        if (elem.name === event.target.name) {
          // eslint-disable-next-line no-console
          elem.selected = event.target.value
        }
      })
      // eslint-disable-next-line no-console
      console.log(this.product)
    },
    updateSelectedMulti(event) {
      // eslint-disable-next-line no-console
      console.log(event)
      this.product.otherOptions.forEach((elem) => {
        // eslint-disable-next-line no-console
        if (elem.name === event.target.name) {
          // eslint-disable-next-line no-console
          elem.selected = event.target.value
        }
      })
      // eslint-disable-next-line no-console
      console.log(this.product)
    },
  },
}
</script>

<style>
.max-h-90 {
  max-height: 75vh !important;
}
</style>
