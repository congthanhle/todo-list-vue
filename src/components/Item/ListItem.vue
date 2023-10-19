<script setup lang="ts">
import {defineEmits} from "vue";
import Item from "@components/Item/index.vue";
import { ItemType } from '@/data-types/item';

const emits = defineEmits(["sendIdDelItem", "sendEditItem"]);

 defineProps<{
  items: ItemType[]
}>()

// Operation to handle item deletion
const handleDeleteItem = (itemId: number) => {
  emits('sendIdDelItem', itemId)
}

// Processes updating the edited content
const handleEditItem = (itemEdited: ItemType) => {
  emits('sendEditItem', itemEdited)
}

</script>

<template>
  <div class="panel panel-success" >
    <div class="panel-heading">List Item</div>
    <table class="table table-hover">
      <thead>
        <tr>
          <th :style="{ 'width': '10%' }" class="text-center">#</th>
          <th>Name</th>
          <th :style="{ 'width': '15%' }" class="text-center">Level</th>
          <th :style="{ 'width': '15%' }">Action</th>
        </tr>
      </thead>
      <tbody>
        <Item v-for="item in items" :key="item.id" :item=item @sendIdDelItem="handleDeleteItem"
          @sendEditItem="handleEditItem" ></Item>
      </tbody>
    </table>
  </div>
</template>

<style scoped></style>