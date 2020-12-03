<template>
  <ul class="list-group">
    <shopping-list-single-item
      v-for="listItem in shoppingList"
      :key="listItem.id"
      :listItem="listItem"
    />

    <li v-if="shoppingList.length === 0" class="list-group-item">
      There is nothing on this Shopping cart for this filter.
    </li>

    <shopping-list-footer v-if="shoppingList.length !== 0" />

    <shopping-list-filters />
  </ul>
</template>

<script>
import { computed, inject, provide, ref } from "vue";
import ShoppingListSingleItem from "./ShoppingListSingleItem.vue";
import ShoppingListFooter from "./ShoppingListFooter.vue";
import ShoppingListFilters from "./ShoppingListFilters.vue";
export default {
  components: {
    ShoppingListSingleItem,
    ShoppingListFooter,
    ShoppingListFilters,
  },
  setup() {
    // First, let's refer our local obj to the parent ShoppingList
    const filteredShoppingList = inject("shoppingList");
    //this will be my initial filter, to display all items
    const selectedFilter = ref("all");
    //let us add these cases to shoppingList
    const shoppingList = computed(() => {
      if (selectedFilter.value === "all") {
        return filteredShoppingList.value;
      }
      if (selectedFilter.value === "active") {
        return filteredShoppingList.value.filter(
          (item) => item.state === false
        );
      }
      if (selectedFilter.value === "completed") {
        return filteredShoppingList.value.filter((item) => item.state === true);
      }
    });
    //This selectedFilter obj will be available for the child comp in this section
    provide("selectedFilter", selectedFilter);

    return { shoppingList };
  },
};
</script>

<style></style>
