<script setup>
import { ref } from 'vue';

// 試完成以下功能：
//  1. 點擊卡片，卡片會翻開 (已完成)
//  2. 點擊兩張不同的卡片，卡片會翻回去 
//  3. 點擊兩張相同的卡片，卡片會消失
//  4. 當所有卡片都消失時，顯示「恭喜破關，再來一局？」的對話框，按下確定後重置遊戲
//  5. 將卡片獨立抽出為 Card.vue 元件

const cards = ref([]);
const openedCard = ref([]);
const openedCardNum = ref([]); //記牌

// 遊戲初始化，洗牌
const gameInit = () => {
  const numArr = [...new Array(16).keys()].map(i => ++i);
  numArr.sort(() => Math.random() - 0.5);
  cards.value = numArr.map(d => (d % 8) + 1);
  openedCard.value = [];
}

const clickHandler = (idx ,n) => {    
  // openedCard.value= [];
  // openedCardNum.value= [];
  console.log(cards.value);
  openedCard.value.push(idx);
  openedCardNum.value.push(n);
  // console.log(n);
  console.log(openedCardNum.value);
  // console.log('----------------');
  if(openedCardNum.value[0]== openedCardNum.value[1]){
    console.log('一樣!');
    cards.value[cardNum] = 0;
  }
  // 一秒後將 openedCard 清空 (牌面覆蓋回去)
  if(openedCard.value.length == 2){
    window.setTimeout(() => {
    openedCard.value = [];
    openedCardNum.value = [];
  }, 1200);
  }
}
</script>

<template>
  <div class="bg-emerald-900 h-[100vh] w-full top-0 left-0 z-10 absolute">

    <div class="my-10 text-white text-center ">
      <div class="mb-8 text-5xl">五倍對對碰</div>
      <button 
        @click.once="gameInit"
        class="rounded font-bold bg-blue-500 mx-6 text-white py-2 px-4 hover:bg-blue-700">開始</button>
    </div>

    <div class="rounded-xl mx-auto border-4 mt-12 grid grid-flow-col p-10 w-[900px] gap-2 grid-rows-4">
      
      <div 
        v-for="(n, idx) in cards"
        :key="n"
        class="flip-card"
        :class="{
          'open': openedCard.includes(idx)
        }"
        @click="clickHandler(idx, n)">
        <div class="flip-card-inner" v-if="cards[idx] > 0">
          <div class="flip-card-front">{{ n }}</div>
          <div class="flip-card-back">
            <img :src="`./img/cat-0${n}.jpg`" alt="">
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<style scoped src="./MatchGame.css"></style>