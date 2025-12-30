<script setup lang="ts">
import { ref } from 'vue'

// 1. 단순한 변수는 데이터가 변해도 화면이 안 바뀝니다.
let count1 = 0 

// 2. ref를 사용해야 Vue가 "어! 데이터 변했네? 화면 다시 그려야지!"라고 눈치를 챕니다.
// <number>는 TypeScript에게 이 값은 '숫자'라고 명시하는 거예요.
const count2 = ref<number>(0)

const increase = () => {
  count1++ // 콘솔에는 찍히지만 화면은 그대로입니다.
  count2.value++ // .value를 수정하면 화면이 자동으로 바뀝니다!
  console.log('일반 변수:', count1, '반응형 ref:', count2.value)
}
</script>

<template>
  <div>
    <p>일반 변수 (안 변함): {{ count1 }}</p>
    <p>반응형 변수 (변함): {{ count2 }}</p>
    <button @click="increase">1씩 증가</button>
  </div>
</template>