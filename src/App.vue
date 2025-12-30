<script setup lang="ts">
import { ref } from 'vue'
import TodoItem from './components/TodoItem.vue' // 자식 컴포넌트 불러오기

// 1. lang="ts": <script> 태그에 이 속성이 있어야 VS Code가 TypeScript 문법을 검사해 줍니다.
//    interface Todo: 윈도우 환경에서 코딩할 때, 만약 text 대신 title이라고 잘못 적으면 VS Code가 즉시 빨간 줄로 알려줄 거예요. 이게 TypeScript의 가장 큰 장점입니다.
//    ref<Todo[]> (제네릭): ref 뒤에 < >를 붙여서 이 배열 안에 어떤 타입이 들어올지 명시합니다. 덕분에 todos.value[0].까지 치면 자동으로 id, text, isDone이 추천 목록에 뜹니다.
// 2. Props (:todo="item"): 부모가 자식에게 데이터를 줄 때 사용합니다. "이 데이터를 가지고 화면을 그려라"라는 지시입니다.
//    Emits (@delete="deleteTodo"): 자식이 부모에게 사건을 알릴 때 사용합니다. "나한테 삭제 버튼이 눌렸으니, 부모님 당신의 데이터를 직접 지워주세요!"라고 요청하는 것입니다.
//    중요: 데이터의 원본은 App.vue에 있기 때문에, 실제 삭제나 수정도 App.vue에서 해야 합니다. (단방향 데이터 흐름)


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

// 할 일 상태 토글 함수
const toggleTodo = (id: number) => {
  const target = todos.value.find(t => t.id === id)
  if (target) target.isDone = !target.isDone
}

// 할 일 삭제 함수
const deleteTodo = (id: number) => {
  todos.value = todos.value.filter(t => t.id !== id)
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

    <ul>
      <TodoItem 
        v-for="item in todos" 
        :key="item.id" 
        :todo="item" 
        @toggle="toggleTodo" 
        @delete="deleteTodo"
      />
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