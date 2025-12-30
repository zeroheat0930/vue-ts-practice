<script setup lang="ts">
import { ref } from 'vue'

// TypeScript에게 이 변수는 'string(문자열)'이라고 알려줍니다.
const message = ref<string>('안녕하세요!')

// 입력창을 비워버리는 함수
const clearMessage = () => {
  message.value = ''
}
</script>

<template>
  <div class="practice">
    <h2>2교시: v-model 연습</h2>
    
    <input v-model="message" placeholder="여기에 아무거나 입력해 보세요" />
    
    <p><strong>실시간 입력 내용:</strong> {{ message }}</p>
    
    <button @click="clearMessage">내용 지우기</button>
  </div>
</template>

<style scoped>
.practice { padding: 20px; }
input { padding: 10px; width: 250px; font-size: 16px; }
p { margin-top: 15px; font-size: 18px; color: #42b883; }
button { margin-top: 10px; padding: 5px 10px; }
</style>