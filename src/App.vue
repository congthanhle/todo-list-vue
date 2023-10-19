<script setup lang="ts">
import { ref } from 'vue';
import Title from "@components/Title/index.vue";
import Search from "@components/Search/index.vue";
import Sort from "@components/Sort/index.vue";
import Form from "@components/Form/index.vue";
import ListItem from "@components/Item/ListItem.vue";
import { ItemType } from "@/data-types/item.ts";
import { items as itemsData } from "./data";

const isAddFormVisible = ref(false);
const items = ref<ItemType[]>(itemsData);
const originalData = ref<ItemType[]>(itemsData);

const handleToggleAddBtn = () => {
  isAddFormVisible.value = !isAddFormVisible.value;
};

const handleHideAddForm = (isVisible: boolean) => {
  isAddFormVisible.value = isVisible;
}

const addNewItem = (item: ItemType) => {
  const newId = items.value.length + 1;
  const newItem = {
    id: newId,
    name: item.name,
    level: Number(item.level)
  }
  items.value = [newItem, ...items.value]
  originalData.value = items.value
}

const handleDeleteItem = (itemId: number) => {
  items.value = items.value.filter(item => item.id !== itemId);
  originalData.value = items.value
}

// Processes updating the edited content
const handleEditItem = (itemEdited: ItemType) => {
  items.value = items.value.map((item: ItemType) => (
    item.id === itemEdited.id ? itemEdited : item
  ));
  originalData.value = items.value
}

const filterData = (query: string) => {
  const searchQuery = query.toLowerCase();
    items.value = originalData.value.filter((item) => {
      return item.name.toLowerCase().includes(searchQuery);
    });
}

const handleSortOption = (option: string) => {
  switch (option) {
    case "1":
      items.value.sort((currentItem, nextItem) => {
        return currentItem.name.localeCompare(nextItem.name);
      });
      break;
    case "2":
      items.value.sort((currentItem, nextItem) => {
        return nextItem.name.localeCompare(currentItem.name);
      });
      break;
    case "3":
      items.value.sort((currentItem, nextItem) => {
        return currentItem.level - nextItem.level;
      });
      break;
    case "4":
      items.value.sort((currentItem, nextItem) => {
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
        <Search @sendSearchQuery="filterData" />
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
        <Form v-if="isAddFormVisible" @sendNewItem="addNewItem" @cancelAddItem="handleHideAddForm" />
      </div>
    </div>
    <ListItem :items="items" @sendIdDelItem="handleDeleteItem" @sendEditItem="handleEditItem" />
  </div>
</template>

<style scoped></style>
