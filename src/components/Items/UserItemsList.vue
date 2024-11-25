<template>
  <div>
    <h3>User Items</h3>
    <div class="list">
      <Item
        v-for="item in items"
        :key="item.id"
        :selected="isSelected(item)"
        :item="item"
        @toggle="handleToggleItem"
      >
        {{ item.name }}
      </Item>
    </div>
  </div>
</template>

<script setup>
import Item from "../common/Item.vue";
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  items: Array,
  selectedItems: Array,
  maxItems: Number,
});

const emit = defineEmits(["update:selectedItems"]);

const isSelected = (item) => props.selectedItems.includes(item);

const handleToggleItem = (item) => {
  const newSelection = [...props.selectedItems];
  const index = newSelection.indexOf(item);
  if (index !== -1) {
    newSelection.splice(index, 1);
  } else if (newSelection.length < props.maxItems) {
    newSelection.push(item);
  }
  emit("update:selectedItems", newSelection);
};
</script>

<style scoped>
@import "@/assets/styles/_lists.css";
</style>