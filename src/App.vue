<script setup lang="ts">
import { ref } from 'vue'

// 1. 리스트에 들어갈 데이터의 타입을 정의합니다.
interface StudyItem {
  id: number;
  title: string;
}

// 2. 여러 개의 데이터를 가진 배열을 ref로 만듭니다.
const studyList = ref<StudyItem[]>([
  { id: 1, title: 'Vue 3 기초 문법 익히기' },
  { id: 2, title: 'TypeScript 인터페이스 이해하기' },
  { id: 3, title: 'v-for로 리스트 만들기' }
])
</script>

<template>
  <div class="practice">
    <h2>4교시: v-for 리스트 연습</h2>
    
    <h3>오늘 배울 내용 목록</h3>
    <ul>
      <li v-for="item in studyList" :key="item.id">
        <span class="badge">{{ item.id }}</span>
        {{ item.title }}
      </li>
    </ul>

    <p v-if="studyList.length === 0">공부할 내용이 아직 없어요!</p>
  </div>
</template>

<style scoped>
.practice { padding: 20px; font-family: sans-serif; }
ul { list-style: none; padding: 0; }
li { 
  padding: 10px; 
  margin-bottom: 5px; 
  background-color: #42b883; 
  border-left: 5px solid #42b883;
}
.badge {
  background-color: #42b883;
  color: white;
  padding: 2px 6px;
  border-radius: 4px;
  margin-right: 8px;
  font-size: 12px;
}
</style>