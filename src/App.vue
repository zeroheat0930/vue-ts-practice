<script setup lang="ts">
import { ref } from 'vue'

// 1. 데이터 타입 정의 (TypeScript)
interface Todo {
  id: number
  text: string
  isDone: boolean
}

// 2. 반응형 데이터 (ref)
const userInput = ref<string>('') // 입력창과 연결될 변수
const todoList = ref<Todo[]>([])   // 할 일들이 담길 배열

// 3. 할 일 추가 함수 (Logic)
const addTodo = () => {
  if (userInput.value.trim() === '') return // 빈 값은 추가 안 함

  const newTodo: Todo = {
    id: Date.now(), // 고유한 ID를 위해 현재 시간을 사용
    text: userInput.value,
    isDone: false
  }

  todoList.value.push(newTodo) // 배열에 추가
  userInput.value = ''         // 입력창 비우기 (양방향 바인딩 덕분에 화면도 비워짐)
}

// 4. 할 일 삭제 함수
const deleteTodo = (id: number) => {
  // 클릭한 ID와 다른 항목들만 남겨서 새로운 배열을 만듦
  todoList.value = todoList.value.filter(todo => todo.id !== id)
}
</script>

<template>
  <div class="todo-app">
    <h1>✅ My Todo List</h1>

    <div class="input-group">
      <input 
        v-model="userInput" 
        @keyup.enter="addTodo"
        placeholder="할 일을 입력하고 엔터를 치세요" 
      />
      <button @click="addTodo">추가</button>
    </div>

    <ul v-if="todoList.length > 0">
      <li v-for="todo in todoList" :key="todo.id">
        <div class="todo-content">
          <input type="checkbox" v-model="todo.isDone" />
          <span :class="{ completed: todo.isDone }">{{ todo.text }}</span>
        </div>
        <button class="del-btn" @click="deleteTodo(todo.id)">삭제</button>
      </li>
    </ul>

    <p v-else class="empty-msg">할 일이 없습니다. 새로운 일을 추가해 보세요!</p>
  </div>
</template>

<style scoped>
/* 앱 전체 레이아웃 */
.todo-app {
  max-width: 450px;
  margin: 50px auto;
  padding: 20px;
  background: #e9a3a3;
  border-radius: 12px;
  box-shadow: 0 10px 25px rgba(0,0,0,0.1);
  font-family: 'Malgun Gothic', sans-serif;
}

h1 { color: #2c3e50; text-align: center; }

/* 입력창 스타일 */
.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
input[type="text"] {
  flex: 1;
  padding: 10px;
  border: 2px solid #eee;
  border-radius: 6px;
  outline: none;
}
input[type="text"]:focus { border-color: #42b883; }

/* 추가 버튼 */
button {
  padding: 10px 15px;
  background: #42b883;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

/* 리스트 스타일 */
ul { list-style: none; padding: 0; }
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px;
  border-bottom: 1px solid #f1f1f1;
}
.todo-content { display: flex; align-items: center; gap: 10px; }

/* 완료된 항목 스타일 */
.completed {
  text-decoration: line-through;
  color: #bbb;
}

/* 삭제 버튼 */
.del-btn {
  background: #ff5e5e;
  padding: 5px 10px;
  font-size: 12px;
}

.empty-msg { text-align: center; color: #999; margin-top: 30px; }
</style>