<template>
    <div class="p-4">
        <h1 class="text-2xl font-bold mb-4">待辦清單</h1>
        <div class="mb-4">
            <input
                v-model="newTodo"
                @keyup.enter="addTodo"
                type="text"
                placeholder="新增待辦事項"
                class="border p-2 rounded mr-2"
            />
            <button @click="addTodo" class="bg-blue-500 text-white px-4 py-2 rounded">新增</button>

            <ul class="mt-4 space-y-2">
                <li v-for="todo in todos" :key="todo.id" class="flex items-center justify-between">
                    <div>
                        <input type="checkbox" v-model="todo.completed" @change="updateTodo(todo)" />
                        <span :class="{ 'line-through': todo.completed}">{{ todo.title }}</span>
                    </div>
                    <button @click="deleteTodo(todo.id)" class="bg-red-500 text-white px-2 py-1 rounded">刪除</button>
                </li>
            </ul>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
const todos = ref([]);
const newTodo = ref('');
const BASE_URL = 'http://localhost:8080'; // API 基礎 URL
axios.defaults.baseURL = BASE_URL;
axios.defaults.headers.common['Content-Type'] = 'application/json';

//查詢所有清單
const fetchTodos = async () => {
    const res = await axios.get('/api/todos');
    todos.value = res.data;
}

//新增清單任務
const addTodo = async () => {
  if (!newTodo.value.trim()) return
  await axios.post('/api/todos', {
    title: newTodo.value,
    completed: false
  })
  newTodo.value = ''
  fetchTodos()
}

//更新清單任務
const updateTodo = async (todo) => {
  await axios.put(`/api/todos/${todo.id}`, todo)
  fetchTodos()
}

//刪除清單任務
const deleteTodo = async (id) => {
  await axios.delete(`/api/todos/${id}`)
  fetchTodos()
}

onMounted(fetchTodos)
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
</style>