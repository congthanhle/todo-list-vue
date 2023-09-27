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
                <tr v-for="item in items">
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
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup lang="ts">
import { items } from "../../../data.ts"

</script>

<style scoped></style>