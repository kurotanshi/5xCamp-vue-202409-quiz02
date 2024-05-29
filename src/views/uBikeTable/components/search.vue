<script setup>
    import { defineModel } from 'vue'
    const model = defineModel()
</script>

<template>
    <p class="my-4 pl-2">
        站點名稱搜尋: <input type="text" v-model="model" class="border w-60 p-1 ml-2">
    </p>
</template>
