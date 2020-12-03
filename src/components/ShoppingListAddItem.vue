<template>
  <form @submit.prevent="submitNewItem">
    <div class="form-group">
      <div class="col-md-12">
        <input
          type="text"
          class="form-control"
          placeholder="Please enter your item"
          v-model.trim="itemToAdd"
        />
      </div>
    </div>
  </form>
</template>

<script>
import { inject, ref } from "vue";
export default {
  setup() {
    // Let's bind this new object with the shoppingList on Parent
    const shoppingList = inject("shoppingList");
    //This is an initial object that we will use in the child component
    //to add the new items to the list
    const itemToAdd = ref("");

    // let us create a function to add the new entries to the shopping list
    const submitNewItem = () => {
      //If the value we bind to the form textfield is empty let us ignore this
      if (itemToAdd.value === "") {
        console.log("Can't really add empty items");
        return;
      }

      // This is the object we will insert in the parent shoppingList object
      const newListEntry = {
        itemToAdd: itemToAdd.value,
        state: false,
        id: Date.now(),
      };
      shoppingList.value.push(newListEntry);
      itemToAdd.value = "";
    };
    // As a good practice, always return the functions, properties etc from super
    return { submitNewItem, itemToAdd };
  },
};
</script>

<style></style>
