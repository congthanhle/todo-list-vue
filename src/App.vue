<script setup lang="ts">
import { ref } from 'vue';
import Title from "./components/Title/Title.vue";
import Search from "./components/Search/Search.vue";
import Sort from "./components/Sort/Sort.vue";
import Form from "./components/Form/Form.vue";
import ListItem from "./components/Item/ListItem/ListItem.vue";
import {ItemType} from "./types/item.ts";
import { items } from "./data";

const isButtonVisible = ref(true);
const newItems = ref<ItemType[]>(items)

const handleToggleAddBtn = () => {
  isButtonVisible.value = !isButtonVisible.value;
};

const handleHideAddForm = (isVisible: boolean) => {
  isButtonVisible.value = isVisible
}

const getNewItem = (item: ItemType) => {
    const newId = items.length + 1;
    const newItem = {
      id: newId,
      name: item.name,
      level: Number(item.level),
    }
    newItems.value.push(newItem);
}



</script>

<template>
  <div class="container">
    <Title />
    <div class="row">
      <div class="col-xs-4 col-sm-4 col-md-4 col-lg-4">
        <Search />
      </div>
      <div class="col-xs-3 col-sm-3 col-md-3 col-lg-3">
        <Sort />
      </div>
      <div class="col-xs-5 col-sm-5 col-md-5 col-lg-5">
        <button type="button" class="btn btn-info btn-block marginB10" @click="handleToggleAddBtn">Add Item</button>
      </div>
    </div>
    <div class="row marginB10">
      <div class="col-md-offset-7 col-md-5">
        <Form v-if="isButtonVisible" @sendNewItem="getNewItem" @cancelAddItem="handleHideAddForm"/>
      </div>
    </div>
    <ListItem :newItem="newItems"/>
  </div>
</template>

<style scoped></style>
