<template>
  <table class="table">
    <thead class="bg-blue-400 text-white">
      <tr>
        <th scope="col">Date</th>
        <th scope="col">Amount</th>
        <th scope="col">Category</th>
        <th scope="col"></th>
      </tr>
    </thead>
    <tbody>
      <tr class="p-4 bg-blue-200 text-center">
        <td colspan="4">
          <button class="underline" @click="triggerShowAddBill">Add new</button>
        </td>
      </tr>
      <tr v-for="(bill, index) in bills" :key="index" class="p-4">
        <td>{{bill.date | moment("DD/MM/YYYY")}}</td>
        <td>&pound;{{bill.amount}}</td>
        <td>{{bill.category}}</td>
        <td>
          <button class="text-red-600" @click="removeBill(index)">𝗫</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "BillsTable",
  props: ["bills"],
  methods: {
    removeBill: function (index) {
      this.$emit("removeBill", index);
    },
    triggerShowAddBill: function () {
      this.$emit("triggerShowAddBill");
    },
  },
};
</script>
