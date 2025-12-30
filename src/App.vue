<script setup lang="ts">
import { ref } from 'vue'

// 1. TypeScript 인터페이스 정의
// '할 일' 데이터가 어떤 모양이어야 하는지 규칙을 정합니다.
interface Todo {
  id: number
  text: string
  isDone: boolean
}

// 2. 반응형 상태(State) 관리
// ref<Todo[]>는 "이 변수는 Todo 객체들이 담긴 배열이다"라고 선언하는 것입니다.
const todos = ref<Todo[]>([
  { id: 1, text: 'TypeScript 환경 설정 완료하기', isDone: true },
  { id: 2, text: 'Vue 3 기본 문법 익히기', isDone: false }
])

// 입력창의 텍스트를 저장할 변수 (타입은 string)
const userInput = ref<string>('')

// 3. 할 일 추가 함수
const addNewTodo = () => {
  if (userInput.value.trim() === '') return

  const newTodo: Todo = {
    id: Date.now(),
    text: userInput.value,
    isDone: false
  }

  todos.value.push(newTodo)
  userInput.value = '' // 입력창 초기화
}
</script>

<template>
  <div class="app-container">
    <h1>📝 My Vue 3 + TS 리스트</h1>

    <div class="input-box">
      <input 
        v-model="userInput" 
        @keyup.enter="addNewTodo"
        placeholder="할 일을 입력하고 Enter!" 
      />
      <button @click="addNewTodo">추가</button>
    </div>

    <ul>
      <li v-for="item in todos" :key="item.id">
        <input type="checkbox" v-model="item.isDone" />
        <span :class="{ completed: item.isDone }">{{ item.text }}</span>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.app-container {
  max-width: 400px;
  margin: 2rem auto;
  font-family: Arial, sans-serif;
}
.input-box {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
input {
  flex: 1;
  padding: 8px;
}
.completed {
  text-decoration: line-through;
  color: #888;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 0;
  border-bottom: 1px solid #eee;
}
</style>