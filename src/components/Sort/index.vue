<script setup lang="ts">
import { ref, defineEmits } from "vue";

const labelText = ref("");

const emits = defineEmits(["sendSortOption"]);

// Send sorting requests to the parent component when options change
const handleSortOption = (value: string) => {
  switch (value) {
    case "1":
      labelText.value = "Name - ASC";
      emits("sendSortOption", value);
      break;
    case "2":
      labelText.value = "Name - DESC";
      emits("sendSortOption", value);
      break;
    case "3":
      labelText.value = "Level - ASC";
      emits("sendSortOption", value);
      break;
    case "4":
      labelText.value = "Level - DESC";
      emits("sendSortOption", value);
      break;
    default:
      labelText.value = "NAME - DESC";
      break;
  }
};
</script>


<template>
    <div class="dropdown">
      <button
        class="btn btn-default dropdown-toggle marginR5 "
        type="button"
        data-toggle="dropdown"
        aria-haspopup="true"
        aria-expanded="true"
      >
        Sort by <span class="caret" />
      </button>
      <ul class="dropdown-menu">
        <li><a @click="handleSortOption('1')" role="button">Name ASC</a></li>
        <li><a @click="handleSortOption('2')" role="button">Name DESC</a></li>
        <li role="separator" class="divider" />
        <li><a @click="handleSortOption('3')" role="button">Level ASC</a></li>
        <li><a @click="handleSortOption('4')" role="button">Level DESC</a></li>
      </ul>
      <span class="label label-success label-medium">{{ labelText }}</span>
    </div>
  </template>
  

<style scoped></style>