<template>
  <div class="h-100 w-full flex items-center justify-center font-sans">
    <div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
      <div class="mb-4">
        <h1 class="text-gray-800 text-3xl">Enter a new bill</h1>
        <p></p>
        <div class="flex mt-4">
          <DatePicker
            wrapper-class="shadow appearance-none border rounded w-full mr-4 text-gray-700"
            input-class="py-2 px-3"
            v-model="date"
          ></DatePicker>
          <input
            class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-gray-700"
            placeholder="Set amount"
            v-model="amount"
          />
          <select class="shadow border rounded py-2 px-3 mr-4 text-gray-700" v-model="category">
            <option v-for="category in categories" :value="category" :key="category">
              {{
              category
              }}
            </option>
          </select>
          <button
            class="flex-no-shrink p-2 border-2 rounded bg-teal-600 text-white border-teal-700 hover:text-white hover:bg-teal-500"
            @click="handleClick"
          >Add</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import DatePicker from "vuejs-datepicker";

export default {
  name: "AddBill",
  components: {
    DatePicker,
  },
  props: ["categories"],
  data: function () {
    return {
      date: new Date(),
      category: this.categories[0],
      amount: 0,
    };
  },
  methods: {
    handleClick: function () {
      if (!this.date) {
        alert("Enter a date");
        return;
      }
      if (!this.amount) {
        alert("Enter an amount");
        return;
      }

      this.$emit("addBill", {
        date: this.date,
        category: this.category,
        amount: parseInt(this.amount, 10),
      });
    },
  },
};
</script>
