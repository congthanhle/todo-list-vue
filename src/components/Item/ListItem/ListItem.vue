<script setup lang="ts">
import { ref, computed } from "vue";
import Item from "../Item/Item.vue";
import { ItemType } from '../../../types/item';

const props = defineProps<{
    newItems: ItemType[]
    filteredItems: ItemType[]
}>()

const items = ref<ItemType[]>(props.newItems.sort((a, b) => {
    return b.name.localeCompare(a.name); 
}));

// Change the value displayed when filtering
const itemsToDisplay = computed(() => {
    return props.filteredItems.length !== 0 ? props.filteredItems : props.newItems;
});

// Operation to handle item deletion
const handleDeleteItem = (itemId: number) => {
    items.value = items.value.filter(item => item.id !== itemId);
}

// Processes updating the edited content
const handleEditItem = (itemEdited: ItemType) => {
    items.value = items.value.map((item: ItemType) => (
        item.id === itemEdited.id ? itemEdited : item
    ));
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
                <Item v-for="item in itemsToDisplay" :key="item.id" :item=item @sendIdDelItem="handleDeleteItem"
                    @sendEditItem="handleEditItem"></Item>
            </tbody>
        </table>
    </div>
</template>

<style scoped></style>