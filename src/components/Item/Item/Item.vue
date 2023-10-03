<script setup lang="ts">
import { defineEmits, ref } from 'vue';
import { ItemType } from '../../../data-types/item';
import ItemEdit from '../ItemEdit/ItemEdit.vue';

const emits = defineEmits(["sendIdDelItem", "sendEditItem"]);

const props = defineProps<{
    item: ItemType
}>()

const isEditMode = ref(false);
// Handle the action of pressing the delete button
const handleDeleteClick = () => {
    const itemId = props.item.id;
    emits('sendIdDelItem', itemId);
}

// Turn on editing mode for the current item
const handleEditClick = () => {
    isEditMode.value = true;
}

//Handle when pressing the cancel button
const cancelEditItem = (isEdit: boolean) => {
    isEditMode.value = isEdit;
}

//Send the item to be edited to the parent component
const sendEditItem = (item: ItemType) => {
    emits('sendEditItem', item);
}

</script>

<template>
    <tr v-if="!isEditMode">
        <td class="text-center">{{ item.id }}</td>
        <td>{{ item.name }}</td>
        <td class="text-center">
            <span v-if="item.level === 0" class="label label-default">Low</span>
            <span v-else-if="item.level === 1" class="label label-info">Medium</span>
            <span v-else-if="item.level === 2" class="label label-danger">High</span>
        </td>
        <td>
            <button type="button" class="btn btn-warning btn-sm marginR5" @click="handleEditClick">Edit</button>
            <button type="button" class="btn btn-danger btn-sm" @click="handleDeleteClick">Delete</button>
        </td>
    </tr>
    <ItemEdit :item="item"  @cancelEditedItem="cancelEditItem" @sendEditedItem="sendEditItem" v-else/>
</template>

<style scoped></style>