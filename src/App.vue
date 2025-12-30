<script setup lang="ts">
import { ref } from 'vue'

// v-if: 아예 없애버린다. (보여줄 일이 거의 없을 때 사용), 조건이 거짓이면 아예 HTML 태그 자체가 사라집니다. (성능 절약)
// v-show: 투명 인간으로 만든다. (아주 자주 껐다 켰다 할 때 사용), HTML은 그대로 두고 CSS의 display: none으로 눈에만 안 보이게 합니다.

// 1. 보여줄지 말지 결정하는 '스위치' 변수 (Boolean 타입)
const isVisible = ref<boolean>(true)

// 스위치를 껐다 켰다 하는 함수
const toggle = () => {
  isVisible.value = !isVisible.value
}
</script>

<template>
  <div class="practice">
    <h2>3교시: 조건부 렌더링 연습 (수정본)</h2>
    
    <button @click="toggle">
      {{ isVisible ? '숨기기' : '보여주기' }}
    </button>

    <hr />

    <div v-if="isVisible" class="box if-box">
      <h3>v-if 상자</h3>
      <p>제가 보이나요? 저는 조건이 안 맞으면 아예 소멸합니다.</p>
    </div>
    <p v-else>상자들이 모두 숨겨졌습니다!</p>

    <div v-show="isVisible" class="box show-box">
      <h3>v-show 상자</h3>
      <p>저는 안 보여도 사실 HTML 안에 숨어있답니다.</p>
    </div>
  </div>
</template>

<style scoped>
.practice { padding: 20px; }
.box {
  padding: 15px;
  margin: 10px 0;
  border-radius: 8px;
  color: white;
}
.if-box { background-color: #42b883; }
.show-box { background-color: #35495e; }
button { padding: 10px 20px; cursor: pointer; }
</style>