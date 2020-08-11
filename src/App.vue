<template>
  <main>
    <AddCategory v-if="shouldShowAddCategory" v-on:addCategory="addCategory" />
    <div v-else>
      <NavBar />
      <div class="container flex">
        <div class="w-1/2">
          <BillsTable />
        </div>
        <div class="w-1/2">
          <Chart :bills="activeBills" />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import AddCategory from "./components/AddCategory.vue";
import BillsTable from "./components/BillsTable.vue";
import Chart from "./components/Chart.vue";
import NavBar from "./components/NavBar.vue";
import "@/assets/css/tailwind.css";

export default {
  name: "App",
  components: {
    AddCategory,
    BillsTable,
    Chart,
    NavBar,
  },
  data() {
    return {
      bills: [],
      categories: [],
      shouldShowAddCategory: true,
    };
  },
  methods: {
    addCategory(category) {
      this.categories.push(category);
      this.shouldShowAddCategory = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
