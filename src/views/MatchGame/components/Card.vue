<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  cardNumber: {
    type: Number,
    required: true
  },
  isOpen: {
    type: Boolean,
    required: true
  },
  isVisible: {
    type: Boolean,
    required: true
  }
});
</script>
<template>
  <div class="flip-card" :class="{ 'open': isOpen }" >
    <div class="flip-card-inner" v-if="isVisible">
      <div class="flip-card-front"></div>
      <div class="flip-card-back">
        <img :src="`./img/cat-0${cardNumber}.jpg`" alt="">
      </div>
    </div>
  </div>
</template>