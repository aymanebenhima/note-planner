<template>
  <div class="filter-nav">
      <button :class="{ active: current === 'all' }" @click="updateFilter('all')">View All</button>
      <button :class="{ active: current === 'completed' }" @click="updateFilter('completed')">Completed</button>
      <button :class="{ active: current === 'ongoing' }" @click="updateFilter('ongoing')">Ongoing</button>
  </div>
</template>

<script>
export default {
    props: ['current'],
    methods: {
        updateFilter(by) {
            this.$emit('filterChange', by)
        }
    },
}
</script>

<style>
.filter-nav button {
  background: none;
  border: none;
  color: #7f8c8d;
  outline: none;
  font-size: 12px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active {
    color: #34495e;
}
</style>