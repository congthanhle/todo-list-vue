<script setup lang="ts">
import { ref } from "vue";
import Item from "../Item/Item.vue";
import { ItemType } from '../../../types/item';

const props = defineProps<{
    newItems: ItemType[]
}>()

const items = ref<ItemType[]>(props.newItems);

const handleDeleteItem = (itemId: number) => {
    items.value = items.value.filter(item => item.id !== itemId)
}

const handleEditItem = (item: ItemType) => {
    console.log(item)
}

</script>
<template>
    <div class="panel panel-success">
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
                    @sendIdEditItem="handleEditItem"></Item>
            </tbody>
        </table>
    </div>
</template>

<style scoped></style>