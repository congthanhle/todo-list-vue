<script setup lang="ts">
import { ref } from 'vue';
import Title from "@components/Title/index.vue";
import Search from "@components/Search/index.vue";
import Sort from "@components/Sort/index.vue";
import Form from "@components/Form/index.vue";
import ListItem from "@components/Item/ListItem.vue";
import { ItemType } from "@/data-types/item.ts";
import { items } from "./data";

const isAddFormVisible = ref(false);
const newItems = ref<ItemType[]>(items);
const filteredItems = ref<ItemType[]>([]);

const handleToggleAddBtn = () => {
  isAddFormVisible.value = !isAddFormVisible.value;
};

const handleHideAddForm = (isVisible: boolean) => {
  isAddFormVisible.value = isVisible;
}

const getNewItem = (item: ItemType) => {
  const newId = items.length + 1;
  const newItem = {
    id: newId,
    name: item.name,
    level: Number(item.level)
  }
  newItems.value.push(newItem);
}

const filteredData = (query: string) => {
  const searchQuery = query.toLowerCase();
  filteredItems.value = newItems.value.filter((item) => {
    return item.name.toLowerCase().includes(searchQuery);
  });
}

const handleSortOption = (option: string) => {
  newItems.value = filteredItems.value.length !== 0 ? filteredItems.value : newItems.value;
  switch (option) {
    case "1":
      newItems.value.sort((currentItem, nextItem) => {
        return currentItem.name.localeCompare(nextItem.name);
      });
      break;
    case "2":
      newItems.value.sort((currentItem, nextItem) => {
        return nextItem.name.localeCompare(currentItem.name);
      });
      break;
    case "3":
      newItems.value.sort((currentItem, nextItem) => {
        return currentItem.level - nextItem.level;
      });
      break;
    case "4":
      newItems.value.sort((currentItem, nextItem) => {
        return nextItem.level - currentItem.level;
      });
      break;
    default:

      break;
  }
}

</script>

<template>
  <div class="container">
    <Title />
    <div class="row">
      <div class="col-xs-4 col-sm-4 col-md-4 col-lg-4">
        <Search @sendSearchQuery="filteredData" />
      </div>
      <div class="col-xs-3 col-sm-3 col-md-3 col-lg-3">
        <Sort @sendSortOption="handleSortOption" />
      </div>
      <div class="col-xs-5 col-sm-5 col-md-5 col-lg-5">
        <button type="button" class="btn btn-info btn-block marginB10" @click="handleToggleAddBtn">Add Item</button>
      </div>
    </div>
    <div class="row marginB10">
      <div class="col-md-offset-7 col-md-5">
        <Form v-if="isAddFormVisible" @sendNewItem="getNewItem" @cancelAddItem="handleHideAddForm" />
      </div>
    </div>
    <ListItem :items="newItems" :filteredItems="filteredItems" />
  </div>
</template>

<style scoped></style>
