<template>
    <div>
      <h3>Selected Item From Available</h3>
      <p>
        {{ selectedAvailableItem?.name || "No item selected" }}
      </p>
    </div>
</template>

<script setup>
  import { defineProps } from "vue";
  
  const props = defineProps({
    selectedAvailableItem: Object
  });
</script>
