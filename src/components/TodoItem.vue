<script setup lang="ts">
// 1. 타입을 다시 정의하거나 가져옵니다 (연습을 위해 우선 정의)
interface Todo {
  id: number
  text: string
  isDone: boolean
}

// 2. 부모로부터 받을 데이터 정의 (Props)
// defineProps<{ 속성명: 타입 }>() 형식을 사용합니다.
const props = defineProps<{
  todo: Todo
}>()

// 3. 부모에게 보낼 신호 정의 (Emits)
// "나 삭제됐어!", "나 체크됐어!"라고 부모에게 알립니다.
const emit = defineEmits<{
  (e: 'toggle', id: number): void
  (e: 'delete', id: number): void
}>()
</script>

<template>
  <li class="todo-item">
    <input 
      type="checkbox" 
      :checked="todo.isDone" 
      @change="emit('toggle', todo.id)" 
    />
    
    <span :class="{ completed: todo.isDone }">
      {{ todo.text }}
    </span>

    <button class="del-btn" @click="emit('delete', todo.id)">삭제</button>
  </li>
</template>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 0;
  border-bottom: 1px solid #eee;
}
.completed {
  text-decoration: line-through;
  color: #888;
}
.del-btn {
  margin-left: auto;
  background-color: #ff4d4f;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 2px 8px;
  cursor: pointer;
}
</style>