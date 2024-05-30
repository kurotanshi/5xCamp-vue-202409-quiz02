<script setup>
const props = defineProps({
  num: Number,
  show: Boolean,
});

const emit = defineEmits(["change"]);
</script>

<template>
  <div class="flip-card" @click="$emit('change')">
    <div class="flip-card-inner" v-if="show">
      <div class="flip-card-front">{{ num }}</div>
      <div class="flip-card-back">
        <img :src="`./img/cat-0${num}.jpg`" alt="" />
      </div>
    </div>
  </div>
</template>

<style scoped src="@/views/MatchGame/MatchGame.css"></style>
