<script setup>
import { ref, watch } from 'vue';
import Card from './Card.vue';

// 試完成以下功能：
//  1. 點擊卡片，卡片會翻開 (已完成)
//  2. 點擊兩張不同的卡片，卡片會翻回去 
//  3. 點擊兩張相同的卡片，卡片會消失
//  4. 當所有卡片都消失時，顯示「恭喜破關，再來一局？」的對話框，按下確定後重置遊戲
//  5. 將卡片獨立抽出為 Card.vue 元件

const cards = ref([]);
const openedCard = ref([]);

// 遊戲初始化，洗牌
const gameInit = () => {
  const numArr = [...new Array(16).keys()].map(i => ++i);
  numArr.sort(() => Math.random() - 0.5);
  cards.value = numArr.map(d => (d % 8) + 1);
  openedCard.value = [];
}

const clickHandler = (idx) => {
  // 同張的卡片，則翻回去
  if(
    openedCard.value.length === 1 &&
    openedCard.value.includes(idx)
  ) {
    openedCard.value = [];
    return;
  }
  // 放入已翻開的卡片
  openedCard.value = [...openedCard.value, idx];
}

watch(openedCard, (selectedCards) => {
  if (selectedCards.length === 2) { // 當選擇兩張卡片時
    setTimeout(() => { // 等卡片翻開的動畫結束後
      const [firstCard, secondCard] = selectedCards;
      if (cards.value[firstCard] === cards.value[secondCard]) { // 當兩張卡片相同時，設定為 0
        cards.value[firstCard] = 0;
        cards.value[secondCard] = 0;
      }
      // 當所有卡片都消失時，顯示「恭喜破關，再來一局？」的對話框，按下確定後重置遊戲
      if (
        cards.value.every(card => card === 0) &&
        confirm("恭喜破關，再來一局？")
      ) {
        gameInit();
      }
      // 清除已翻開的卡片
      openedCard.value = [];
    }, 1000);
  }
});

</script>

<template>
  <div class="bg-emerald-900 h-[100vh] w-full top-0 left-0 z-10 absolute">

    <div class="my-10 text-white text-center ">
      <div class="mb-8 text-5xl">五倍對對碰</div>
      <button 
        @click="gameInit"
        class="rounded font-bold bg-blue-500 mx-6 text-white py-2 px-4 hover:bg-blue-700">開始</button>
    </div>

    <div class="rounded-xl mx-auto border-4 mt-12 grid grid-flow-col p-10 w-[900px] gap-2 grid-rows-4">
      
      <Card
        v-for="(n, idx) in cards"
        :key="idx"
        :idx="idx"
        :n="n"
        :isOpen="openedCard.includes(idx)"
        :isVisible="cards[idx] > 0"
        @clickHandler="clickHandler"
      />

    </div>
  </div>
</template>