<script setup>
const searchTextVal = defineModel('searchText');

</script>
<template>
    <p class="mb-3">
    站點名稱搜尋: <input class="border" type="text" v-model="searchTextVal">
    </p>
</template>