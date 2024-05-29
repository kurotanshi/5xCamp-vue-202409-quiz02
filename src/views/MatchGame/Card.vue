<script setup>
  const props = defineProps({
    idx: Number,
    n: Number,
    isOpen: Boolean,
    isVisible: Boolean
  });

const emit = defineEmits(['clickHandler']);

const clickHandler = (idx) => {
  emit('clickHandler', idx);
}

</script>

<template>
  <div 
    class="flip-card"
    :class="{
      'open': isOpen
    }"
    @click="clickHandler(idx)">
    <div class="flip-card-inner" v-if="isVisible">
      <div class="flip-card-front">{{ n }}</div>
      <div class="flip-card-back">
        <img :src="`./img/cat-0${n}.jpg`" alt="">
      </div>
    </div>
  </div>
</template>

<style scoped src="./MatchGame.css"></style>