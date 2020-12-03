<template>
  <div class="card mt-3">
    <div class="card-title text-left p-2 text-uppercase text-secondary">
      <i class="fa fa-filter" aria-hidden="true"></i> Filtered by:
    </div>
    <div class="card-body d-flex justify-content-between align-items-center ">
      <span
        role="button"
        :class="{ currentfilter: selectedFilter == 'active' }"
        @click="setCurrentFilter('active')"
      >
        Active
      </span>
      <span
        role="button"
        :class="{ currentfilter: selectedFilter == 'all' }"
        @click="setCurrentFilter('all')"
      >
        All
      </span>
      <span
        role="button"
        :class="{ currentfilter: selectedFilter == 'completed' }"
        @click="setCurrentFilter('completed')"
      >
        Completed
      </span>
    </div>
  </div>
</template>

<script>
import { inject } from "vue";
export default {
  setup() {
    // let us get a local obj binded to the parent obj
    // to get the current filter that has been selected
    const selectedFilter = inject("selectedFilter");

    // Time to set the current filter with this function
    const setCurrentFilter = (val) => {
      selectedFilter.value = val;
    };
    // Vue 3 best practice, return the dependency to the component
    return { setCurrentFilter, selectedFilter };
  },
};
</script>

<style>
.currentfilter {
  color: #ffd166;
  font-weight: 400;
}
</style>
