<script setup lang="ts">
import { defineEmits, ref } from 'vue';
import { ItemType } from '@/data-types/item.ts'
const emits = defineEmits(["sendEditedItem", "cancelEditedItem"]);

const props = defineProps<{
    item: ItemType,
}>()

// Assign the item's value to the form for editing
const formData = ref({
    name: props.item.name,
    level: props.item.level,
});
// Handle the operation of saving data when pressing the Save button
const handleSaveClick = () => {
    const { name, level } = formData.value;
    const id = props.item.id;
    emits('sendEditedItem', { id, name, level });
    handleCancelClick();
}

// Handle the edit cancellation operation
const handleCancelClick = () => {
    emits('cancelEditedItem', false);
}

</script>
<template>
    <tr>
        <td class="text-center">{{ item.id }}</td>
        <td>
            <input type="text" class="form-control" v-model="formData.name" />
        </td>
        <td class="text-center">
            <select class="form-control" v-model="formData.level">
                <option :value=0>Low</option>
                <option :value=1>Medium</option>
                <option :value=2>High</option>
            </select>
        </td>
        <td>
            <button type="button" class="btn btn-default btn-sm marginR5" @click="handleCancelClick">Cancel</button>
            <button type="button" class="btn btn-success btn-sm" @click="handleSaveClick">Save</button>
        </td>
    </tr>
</template>

<style scoped></style>