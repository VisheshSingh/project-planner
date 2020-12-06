<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{ active: current === 'all' }">
      View all
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: current === 'completed' }"
    >
      Completed
    </button>
    <button
      @click="updateFilter('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  name: 'FilterNav',
  props: ['current'],
  methods: {
    updateFilter(by) {
      this.$emit('filterChange', by);
    },
  },
};
</script>

<style>
.filter-nav button {
  background: none;
  color: #aaa;
  outline: none;
  padding: 10px;
  margin: 0px;
  letter-spacing: 1px;
  text-transform: uppercase;
}
.filter-nav button.active {
  color: #555;
  font-weight: bold;
}
</style>
