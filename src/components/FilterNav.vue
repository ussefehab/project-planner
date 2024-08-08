<template>
  <nav class="filter-nav">
    <button
      @click="filterHandler('all')"
      :class="{ active: current === 'all' }"
    >
      View all
    </button>
    <button
      @click="filterHandler('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >
      Ongoing
    </button>
    <button
      @click="filterHandler('completed')"
      :class="{ active: current === 'completed' }"
    >
      Completed
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    filterHandler(by) {
      this.$emit("filter", by);
    },
  },
};
</script>

<style>
button {
  background: none;
  border: none;
  color: #888;
  font-size: 18px;
  margin-right: 15px;
  cursor: pointer;
}
.filter-nav button.active {
  color: #333;
  font-weight: 700;
}
</style>
