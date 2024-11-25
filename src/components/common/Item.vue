<template>
    <div
        class="item"
        :class="{
            selected: isSelected
        }"
        @click="handleItemClick"
    >
        <slot></slot>
    </div>
</template>

<script setup>
import { defineProps, defineEmits, computed } from "vue";

const props = defineProps({
  item: {
    type: Object,
    required: true,
  },
  selected: {
    type: Boolean,
    default: false,
  }
});

const emit = defineEmits(["toggle"]);

const isSelected = computed(() => props.selected);

const handleItemClick = () => {
  emit("toggle", props.item);
};
</script>

<style scoped>
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
</style>