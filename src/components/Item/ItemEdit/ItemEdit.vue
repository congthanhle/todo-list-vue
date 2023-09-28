<template>
    <tr>
        <td class="text-center">{{ item.id }}</td>
        <td>
            <input type="text" class="form-control" :defaultValue="item.name" />
        </td>
        <td class="text-center">
            <select class="form-control" :value="item.level">
                <option :value=0>Low</option>
                <option :value=1>Medium</option>
                <option :value=2>High</option>
            </select>
        </td>
        <td>
            <button type="button" class="btn btn-default btn-sm">Cancel</button>
            <button type="button" class="btn btn-success btn-sm">Save</button>
        </td>

    </tr>
</template>

<script setup lang="ts">
import { ItemType } from '../../../types/item';

defineProps<{
    item: ItemType,
}>()

</script>

<style scoped></style>