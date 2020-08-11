<template>
  <div>
    <h1>Enter a category of bills</h1>
    <p>e.g. 'Electricity', 'Gas' or 'Internet'</p>
    <input placeholder="Add category" v-model="category" />
    <button @click="handleClick">Add</button>
  </div>
</template>

<script>
export default {
  name: "AddCategory",
  data: function () {
    return {
      category: "",
    };
  },
  methods: {
    handleClick: function () {
      if (!this.category) {
        alert("Enter a category");
        return;
      }
      this.$emit("addCategory", this.category);
    },
  },
};
</script>
