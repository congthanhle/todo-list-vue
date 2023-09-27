<template>
    <div class="dropdown">
        <button class="btn btn-default dropdown-toggle marginR5 " type="button" data-toggle="dropdown" aria-haspopup="true"
            aria-expanded="true">
            Sort by <span class="caret" />
        </button>
        <ul class="dropdown-menu">
            <li><a role="button">Name ASC</a></li>
            <li><a role="button">Name DESC</a></li>
            <li role="separator" class="divider" />
            <li><a role="button">Level ASC</a></li>
            <li><a role="button">Level DESC</a></li>
        </ul>
        <span class="label label-success label-medium">NAME - DESC</span>
    </div>
</template>

<script setup lang="ts">

</script>

<style scoped></style>