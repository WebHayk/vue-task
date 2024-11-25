<template>
    <div>
      <h3>Available Items</h3>
      <div class="list">
        <Item
          v-for="item in items"
          :key="item.id"
          :selected="selectedItem === item"
          :item="item"
          @toggle="handleSelectItem"
        >
          {{ item.name }}
        </Item>
      </div>
    </div>
</template>
  
<script setup>
  import { defineProps, defineEmits } from "vue";
  import Item from "../common/Item.vue";
  
  const props = defineProps({
    items: Array,
    selectedItem: Object,
  });
  
  const emit = defineEmits(["update:selectedItem"]);
  
  const handleSelectItem = (item) => {
    let selectedItem = props.selectedItem === item ? null : item;
    emit("update:selectedItem", selectedItem);
  };
</script>

<style scoped>
@import "@/assets/styles/_lists.css";
</style>