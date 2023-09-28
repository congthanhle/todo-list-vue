<script setup lang="ts">
import { ref, defineEmits } from 'vue';

const emits = defineEmits(["sendSearchQuery"])

const searchQuery = ref('');

const handleSearchQueryChange = () => {
  emits("sendSearchQuery", searchQuery.value);
};

const handleClearQuery = () => {
    searchQuery.value =""
  emits("sendSearchQuery", "");
};
</script>

<template>
    <div class="input-group">
        <input type="text" class="form-control" placeholder="Search item name"  
         v-model="searchQuery" @input="handleSearchQueryChange"/>
        <span class="input-group-btn">
            <button class="btn btn-info" type="button" @click="handleClearQuery">Clear</button>
        </span>
    </div>
</template>

<style scoped></style>