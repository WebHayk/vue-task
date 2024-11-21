<template>
  <div class="container">
    <div>
      <h3>Selected User Items</h3>
      <ul>
        <li v-for="item in selectedUserItems" :key="item.id">
          {{ item.name }}
        </li>
      </ul>
      <p class="selected-label">
        Selected: <b>{{ selectedUserItems.length }} / {{ userItems.length }}</b>
      </p>
    </div>

    <div>
      <h3>Selected Item From Available</h3>
      <p>
        {{ selectedAvailableItem?.name || "No item selected" }}
      </p>
    </div>

    <div>
      <h3>User Items</h3>
      <div class="items-list">
        <div
          v-for="item in userItems"
          :key="item.id"
          class="item"
          :class="{ selected: isItemSelected(item, selectedUserItems) }"
          @click="toggleSelection(item, selectedUserItems, USER_SELECTED_MAX_ITEMS)"
        >
          {{ item.name }}
        </div>
      </div>
    </div>

    <div>
      <h3>Available Items</h3>
      <div class="items-list">
        <div
          v-for="item in availableItems"
          :key="item.id"
          class="item"
          :class="{ selected: selectedAvailableItem === item }"
          @click="selectSingleItem(item)"
        >
          {{ item.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const USER_SELECTED_MAX_ITEMS = 6;

const userItems = ref([
  { id: 1, name: "Shoes 1" },
  { id: 2, name: "Shoes 2" },
  { id: 3, name: "Shoes 3" },
  { id: 4, name: "Shoes 4" },
  { id: 5, name: "T-shirt 1" },
  { id: 6, name: "T-shirt 2" },
  { id: 7, name: "T-shirt 3" },
  { id: 8, name: "T-shirt 4" }
]);

const availableItems = ref([
  { id: 11, name: "Jacket 1" },
  { id: 12, name: "Jacket 2" },
  { id: 13, name: "Jacket 3" },
  { id: 14, name: "Jacket 4" },
  { id: 15, name: "Hoodie 1" },
  { id: 16, name: "Hoodie 2" },
  { id: 17, name: "Hoodie 3" },
  { id: 18, name: "Hoodie 4" }
]);

const selectedUserItems = ref([]);
const selectedAvailableItem = ref(null);

const toggleSelection = (item, list, maxItems) => {
  const index = list.indexOf(item);
  if (index !== -1) {
    list.splice(index, 1);
  } else if (list.length < maxItems) {
    list.push(item);
  }
};

const selectSingleItem = (item) => {
  selectedAvailableItem.value = selectedAvailableItem.value === item ? null : item;
};

const isItemSelected = (item, list) => list.includes(item);
</script>

<style scoped>
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 15px;
  max-width: 900px;
  margin: auto;
  padding: 20px;
  background-color: #f4f4f9;
  border-radius: 8px;
}

h3 {
  color: #333;
  margin-bottom: 10px;
}

.items-list {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.item {
  padding: 10px;
  border: 1px solid #ccc;
  background-color: white;
  border-radius: 4px;
  cursor: pointer;
  text-align: center;
  min-width: 100px;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.item:hover {
  transform: scale(1.05);
}

.selected {
  background-color: #99ee90;
  border-color: #81c784;
}

.selected-label {
  margin-top: 5px;
  color: #555;
}
</style>