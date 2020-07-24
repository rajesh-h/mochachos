<template>
  <div class="container mx-auto">
    <div>
      <table class="table-fixed w-full">
        <thead>
          <tr>
            <th class="w-1/2 px-2 py-2">Title</th>
            <th class="w-1/6 px-2 py-2">Quantity</th>
            <th class="w-1/6 px-2 py-2">Price</th>
            <th class="w-1/6 px-2 py-2">Total</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="px-2 py-2 text-sm md:text-md">{{ product.name }}</td>
            <td class="px-2 py-2 text-sm md:text-md">
              <div class="flex flex-row justify-around items-center">
                <button
                  v-if="checkCart({ _id: product._id })"
                  class="text-md md:text-2xl text-red-600 p-2 font-bold focus:outline-none"
                  @click="
                    addToCart_vx({
                      _id: product._id,
                      name: product.name,
                      img: product.img,
                      price: product.price,

                      qty: -1,
                    })
                  "
                >
                  -
                </button>
                <div
                  v-if="checkCart({ _id: product._id })"
                  class="self-center font-semibold"
                >
                  {{ getQty({ _id: product._id }) }}
                </div>
                <button
                  class="text-md md:text-2xl text-primary p-2 font-bold focus:outline-none"
                  @click="
                    addToCart_vx({
                      _id: product._id,
                      name: product.name,
                      img: product.img,
                      price: product.price,
                      qty: 1,
                    })
                  "
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
        @onUpdateSelectedSingle="updateSelected"
        @onUpdateSelectedMulti="updateSelected"
      />
      <textarea
        id=""
        v-model="product.instructions"
        class="p-2 m-2 bg-primary rounded-md border border-purple-500"
        name=""
        cols="30"
        rows="2"
        placeholder="Special Instructions"
        @change="
          addAdditinalInfo({
            _id: product._id,
            instructions: product.instructions,
            otherOptions: product.otherOptions,
          })
        "
      ></textarea>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style></style>
