<template>
    <div>
        <form class="form-inline">
            <div class="form-group marginR5 ">
                <input type="text" class="form-control" placeholder="Item Name" />
            </div>
            <div class="form-group">
                <select class="form-control marginR5 ">
                    <option v-bind:value="`${0}`">Small</option>
                    <option v-bind:value="2">Medium</option>
                    <option v-bind:value="3">High</option>
                </select>
            </div>
            <button type="button" class="btn btn-primary marginR5 ">Submit</button>
            <button type="button" class="btn btn-default">Cancel</button>
        </form>
    </div>
</template>

<script setup lang="ts">

</script>

<style scoped></style>