<template>
    <div>
      <h3>Selected User Items</h3>
      <ul class="selected-list">
        <li 
            v-for="item in selectedItems"
            :key="item.id"
        >
          {{ item.name }}
        </li>
      </ul>
      <p class="selected-label">
        Selected: <b>{{ selectedItems.length }} / {{ totalItems }}</b>
      </p>
    </div>
</template>
  
<script setup>
  import { defineProps } from "vue";
  
  const props = defineProps({
    selectedItems: Array,
    totalItems: Number,
  });
</script>

<style scoped>
.selected-list {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.selected-label {
  margin-top: 5px;
  color: #555;
}
</style>
  