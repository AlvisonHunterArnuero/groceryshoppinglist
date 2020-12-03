<template>
  <li class="list-group-item d-flex justify-content-between align-items-center">
    <span role="button"> {{ activeItems }} Active item(s) </span>
    <span role="button" @click="deleteCompleted">
      Delete Completed
    </span>
  </li>
</template>

<script>
import { computed, inject } from "vue";
export default {
  setup() {
    const shoppingList = inject("shoppingList");

    const activeItems = computed(() => {
      return shoppingList.value.filter((item) => item.state === false).length;
    });

    const deleteCompleted = () => {
      shoppingList.value = shoppingList.value.filter(
        (item) => item.state === false
      );
    };

    return { shoppingList, activeItems, deleteCompleted };
  },
};
</script>

<style></style>
