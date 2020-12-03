<template>
  <li class="list-group-item d-flex justify-content-between align-items-center">
    <span
      role="button"
      @click="markItemAsCompleted(listItem.id)"
      :class="{ purchased: listItem.state }"
    >
      {{ listItem.itemToAdd }}
    </span>

    <span role="button" @click="deleteItem(listItem.id)">
      <i class="text-danger fa fa-trash" aria-hidden="true"></i>
    </span>
  </li>
</template>

<script>
import { inject } from "vue";
export default {
  //let's capture the props passed by the parent to this child
  props: {
    listItem: {
      type: Object,
      required: true,
    },
  },
  setup() {
    const shoppingList = inject("shoppingList");

    const deleteItem = (id) => {
      shoppingList.value = shoppingList.value.filter((item) => item.id !== id);
    };

    const markItemAsCompleted = (id) => {
      shoppingList.value = shoppingList.value.map((item) => {
        if (item.id === id) {
          item.state = true;
        }
        return item;
      });
    };

    return { deleteItem, markItemAsCompleted };
  },
};
</script>

<style>
.purchased {
  text-decoration: line-through;
  color: rgb(213, 249, 7);
}
</style>
