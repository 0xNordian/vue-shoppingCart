<template>
  <div class="flex justify-center align-center gap-20 mt-60">
    <div class="flex flex-col justify-center items-center">

      <h1 class="mt-6 text-4xl">Add Product</h1>
      <form @submit.prevent="addProduct">
        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-black">
          Product Name:
          <input type="text" v-model="name"
            class="w-[100%] bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 w-1/4" />
        </label>
        <br />
        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-black">
          Quantity:
          <input type="number" v-model.number="quantity"
            class="w-[100%] bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 w-1/4" />
        </label>
        <br />
        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-black">
          Price:
          <input type="number" v-model.number="price"
            class="w-[100%] bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 w-1/4" />
        </label>
        <br />
        <button type="submit"
          class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add</button>
      </form>
    </div>

    <div class="flex justify-center content-center items-center flex-col shadow-md sm:rounded-lg">
      <div>
        <h1 class="text-6xl text-center mb-6">Shopping Cart</h1>
        <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
          <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr class="text-center">
              <th scope="col" class="py-3 px-6">Product</th>
              <th scope="col" class="py-3 px-6">Quantity</th>
              <th scope="col" class="py-3 px-6">Price</th>
              <th scope="col" class="py-3 px-6">Total</th>
              <th scope="col" class="py-3 px-6"></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in items" :key="index"
              class="bg-white border-b dark:bg-gray-900 dark:border-gray-700 text-center">
              <td scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">{{ item.name
              }}
              </td>
              <td scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                <input type="number" v-model.number="item.quantity" @input="updateTotal()"
                  class="bg-white border-b dark:bg-gray-900 dark:border-gray-700 text-center" />
              </td>
              <td>{{ `$${Math.floor(item.price)}` }}</td>
              <td>{{ `$${Math.floor(item.total)}` }}</td>

              <td>
                <button @click="removeItem(index)"
                  class="mr-6 font-medium text-blue-600 dark:text-blue-500 hover:underline">Remove</button>
              </td>
            </tr>
          </tbody>
        </table>
        <p class="text-lg font-bold mt-8">Total: {{ `$${Math.floor(overallTotal)}` }}</p>
        <!-- <p>Total: {{ total }}</p> -->

      </div>



    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      items: [
        { name: "Apples", quantity: 1, price: 9.99, total: 9.99 },
        { name: "Pears", quantity: 2, price: 4.99, total: 9.98 },
      ],
      total: 0,
      name: "",
      quantity: 1,
      price: 0,
    };
  },
  computed: {
    overallTotal() {
      return this.items.reduce((acc, item) => acc + item.total, 0);
    },
  },
  methods: {
    updateTotal() {
      this.items.forEach((item) => {
        item.total = item.quantity * item.price;
      });
    },
    removeItem(index) {
      this.items.splice(index, 1);
      this.updateTotal();
    },
    addProduct() {
      this.items.push({
        name: this.name,
        quantity: this.quantity,
        price: this.price,
        total: this.quantity * this.price,
      });
      this.name = "";
      this.quantity = 1;
      this.price = 0;
      this.updateTotal();
    },
  },
  created() {
    this.updateTotal();
  },
};
</script>
