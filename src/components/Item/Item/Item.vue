<template>
    <td class="text-center">{{ item.id }}</td>
    <td>{{ item.name }}</td>
    <td class="text-center">
        <span v-if="item.level === 0" class="label label-default">Low</span>
        <span v-else-if="item.level === 1" class="label label-info">Medium</span>
        <span v-else-if="item.level === 2" class="label label-danger">High</span>
    </td>
    <td>
        <button type="button" class="btn btn-warning btn-sm marginR5">Edit</button>
        <button type="button" class="btn btn-danger btn-sm">Delete</button>
    </td>
</template>

<script setup lang="ts">
import { ItemType } from '../../../types/item';
defineProps<{
    item: ItemType
}>()
</script>

<style scoped></style>