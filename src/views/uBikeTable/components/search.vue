<script setup>
import { ref } from 'vue';

const searchText = ref('');

const emit = defineEmits(['search']);

const handleSearch = () => {
  emit('search', searchText.value);
};
</script>

<template>
  <p class="mb-3">
    站點名稱搜尋: <input class="border" type="text" v-model="searchText">
    <button @click="handleSearch">搜尋</button>
  </p>
</template>
