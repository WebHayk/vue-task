<template>
  <div class="container">
    <SelectedUserItems
      :selectedItems="selectedUserItems"
      :totalItems="userItems.length"
    />

    <SelectedFromAvailable
      :selectedAvailableItem="selectedAvailableItem"
    />

    <UserItemsList
      :items="userItems"
      :selectedItems="selectedUserItems"
      :maxItems="USER_SELECTED_MAX_ITEMS"
      @update:selectedItems="updateSelectedUserItems"
    />

    <AvailableItemsList
      :items="availableItems"
      :selectedItem="selectedAvailableItem"
      @update:selectedItem="updateSelectedAvailableItem"
    />
  </div>
</template>

<script setup>
import {USER_SELECTED_MAX_ITEMS} from "../core/variables/index.ts";
import SelectedUserItems from "../components/Items/SelectedUserItems.vue";
import SelectedFromAvailable from "../components/Items/SelectedFromAvailable.vue";
import UserItemsList from "../components/Items/UserItemsList.vue";
import AvailableItemsList from "../components/Items/AvailableItemsList.vue";
import {USER_ITEMS, AVAILABLE_ITEMS} from "../core/static/index.ts";
import {ref} from "vue";

const userItems = ref(USER_ITEMS);
const availableItems = ref(AVAILABLE_ITEMS);

const selectedUserItems = ref([]);
const selectedAvailableItem = ref(null);

const updateSelectedUserItems = (items) => {
  selectedUserItems.value = items;
};

const updateSelectedAvailableItem = (item) => {
  selectedAvailableItem.value = item;
};
</script>

<style scoped>
@import "@/assets/styles/_container.css";
</style>