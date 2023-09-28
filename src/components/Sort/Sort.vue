<script setup lang="ts">
import { ref, defineEmits } from "vue";

const labelText = ref("NAME - DESC");

const emits = defineEmits(["sendSortOption"]);

const handleSortOption = (value: string) => {
  switch (value) {
    case "Name ASC":
      labelText.value = "Name - ASC";
      emits("sendSortOption", labelText.value);
      break;
    case "Name DESC":
      labelText.value = "Name - DESC";
      emits("sendSortOption", labelText.value);
      break;
    case "Level ASC":
      labelText.value = "Level - ASC";
      emits("sendSortOption", labelText.value);
      break;
    case "Level DESC":
      labelText.value = "Level - DESC";
      emits("sendSortOption", labelText.value);
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
        <li><a @click="handleSortOption('Name ASC')" role="button">Name ASC</a></li>
        <li><a @click="handleSortOption('Name DESC')" role="button">Name DESC</a></li>
        <li role="separator" class="divider" />
        <li><a @click="handleSortOption('Level ASC')" role="button">Level ASC</a></li>
        <li><a @click="handleSortOption('Level DESC')" role="button">Level DESC</a></li>
      </ul>
      <span class="label label-success label-medium">{{ labelText }}</span>
    </div>
  </template>
  

<style scoped></style>