<template>
  <ul class="list-reset flex justify-center border-b-4 mb-0">
    <li
      class="top-menu-item hover:bg-gray-400"
      :class="[ activeCategory === category ? 'bg-gray-600' : 'bg-gray-200' ]"
      v-for="category in categories"
      :key="category"
      @click="setActiveCategory(category)"
    >{{category}}</li>
    <li
      class="top-menu-item hover:bg-gray-400"
      :class="[ activeCategory === '' ? 'bg-gray-600' : 'bg-gray-200' ]"
      @click="clearActiveCategory()"
    >All</li>
    <li class="top-menu-item bg-gray-200 hover:bg-gray-400" @click="triggerShowAddCategory">➕</li>
  </ul>
</template>

<script>
export default {
  name: "NavBar",
  props: ["categories", "activeCategory"],
  methods: {
    clearActiveCategory() {
      this.$emit("clearActiveCategory");
    },
    setActiveCategory(category) {
      this.$emit("setActiveCategory", category);
    },
    triggerShowAddCategory() {
      this.$emit("triggerShowAddCategory");
    },
  },
};
</script>

<style lang="postcss" scoped>
.top-menu-item {
  @apply p-4 inline uppercase font-black cursor-pointer;
}
</style>
