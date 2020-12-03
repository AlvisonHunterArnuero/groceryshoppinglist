<template>
  <h1 class="text-info">Basic Grocery Shopping List</h1>
  <p class="text-success">
    Made with <b class="text-danger">❤️</b> by Alvison Hunter using Vue 3 -
    November 30th, 2020
  </p>
  <shopping-list-add-item />
  <shopping-list />
</template>

<script>
import { provide, ref, watchEffect } from "vue";
import ShoppingListAddItem from "./ShoppingListAddItem.vue";
import ShoppingList from "./ShoppingList.vue";
export default {
  components: { ShoppingListAddItem, ShoppingList },
  setup() {
    //let us init our shoppingList and use this object as a reference
    // so that the child components can have access to it by the injected method
    const shoppingList = ref([]);
    //let us provide this object now with the same name, now child comp can access it
    provide("shoppingList", shoppingList);

    // let us get the information of the shoppingListItems from the Local Storage object
    if (localStorage.getItem("shoppingList")) {
      shoppingList.value = JSON.parse(localStorage.getItem("shoppingList"));
    }
    //If the shoppingList gets updated, let's capture that and update the lstorItem as well
    //using the watchEffect hook for that, pretty cool feature of this version
    watchEffect(() => {
      localStorage.setItem("shoppingList", JSON.stringify(shoppingList.value));
    });
  },
};
</script>

<style></style>
