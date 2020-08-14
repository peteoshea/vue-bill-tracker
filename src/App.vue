<template>
  <main>
    <AddCategory v-if="shouldShowAddCategory" v-on:addCategory="addCategory" />
    <div v-else>
      <AddBill v-if="shouldShowAddBill" :categories="categories" v-on:addBill="addBill" />
      <div v-else>
        <NavBar
          :activeCategory="activeCategory"
          :categories="categories"
          v-on:clearActiveCategory="clearActiveCategory"
          v-on:setActiveCategory="setActiveCategory"
          v-on:triggerShowAddCategory="triggerShowAddCategory"
        />
        <div class="container flex">
          <div class="w-1/2 bg-gray-100">
            <BillsTable
              :bills="activeBills"
              v-on:removeBill="removeBill"
              v-on:triggerShowAddBill="triggerShowAddBill"
            />
          </div>
          <div class="w-1/2 bg-gray-100">
            <Chart :bills="activeBills" />
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import AddBill from "./components/AddBill.vue";
import AddCategory from "./components/AddCategory.vue";
import BillsTable from "./components/BillsTable.vue";
import Chart from "./components/Chart.vue";
import NavBar from "./components/NavBar.vue";
import "@/assets/css/tailwind.css";
import Vue from "vue";

Vue.use(require("vue-moment"));

export default {
  name: "App",
  components: {
    AddBill,
    AddCategory,
    BillsTable,
    Chart,
    NavBar,
  },
  data() {
    return {
      activeCategory: "",
      bills: [],
      categories: [],
      shouldShowAddBill: false,
      shouldShowAddCategory: false,
    };
  },
  mounted() {
    if (localStorage.getItem("bills")) {
      this.bills = JSON.parse(localStorage.getItem("bills"));
    }
    if (localStorage.getItem("categories")) {
      this.categories = JSON.parse(localStorage.getItem("categories"));
    }
    if (!this.bills.length && !this.categories.length) {
      this.shouldShowAddCategory = true;
    }
  },
  methods: {
    addBill(bill) {
      this.bills.push(bill);
      this.shouldShowAddBill = false;
    },
    addCategory(category) {
      this.categories.push(category);
      this.shouldShowAddCategory = false;
    },
    clearActiveCategory() {
      this.activeCategory = "";
    },
    removeBill(index) {
      this.bills = this.bills
        .slice(0, index)
        .concat(this.bills.slice(index + 1, this.bills.length));
    },
    setActiveCategory(category) {
      this.activeCategory = category;
    },
    triggerShowAddBill() {
      this.shouldShowAddBill = true;
    },
    triggerShowAddCategory() {
      this.shouldShowAddCategory = true;
    },
  },
  watch: {
    bills() {
      localStorage.setItem("bills", JSON.stringify(this.bills));
    },
    categories() {
      localStorage.setItem("categories", JSON.stringify(this.categories));
    },
  },
  computed: {
    activeBills() {
      return this.bills
        .filter((bill) =>
          this.activeCategory ? bill.category === this.activeCategory : true
        )
        .sort((a, b) => (new Date(a.date) < new Date(b.date) ? 1 : -1));
    },
  },
};
</script>
