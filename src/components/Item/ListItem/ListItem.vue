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
                <tr v-for="item in newItem" :key="item.id">
                    <Item :item=item></Item>

                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup lang="ts">
// import { ref } from 'vue';
// import { items as Items } from "../../../data.ts";
import Item from "../Item/Item.vue";
import { ItemType } from '../../../types/item';
// const items = ref(Items);

const props = defineProps<{
    newItem: ItemType[]
}>()

console.log(props.newItem);


</script>

<style scoped></style>