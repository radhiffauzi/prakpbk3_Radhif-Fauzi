<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Makan', done: true },
  { id: id++, text: 'Gosok Gigi', done: true },
  { id: id++, text: 'Cuci Motor', done: false },
  { id: id++, text: 'Meeting Jam 18:00', done: false }
])

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <div class="container">
    <div class="todo-form">
      <h2 class="title">Tambahkan List Anda</h2>
      <form @submit.prevent="addTodo">
        <input v-model="newTodo" required placeholder="New todo" class="input">
        <button type="submit" class="button">Tambah</button>
      </form>
    </div>
    <div class="todo-list">
      <div class="header">
        <h1 class="list-title"><span>My</span><span>List</span></h1>
      </div>
      <ul class="list-items">
        <li v-for="todo in filteredTodos" :key="todo.id" class="list-item">
          <div>
            <input type="checkbox" v-model="todo.done" class="checkbox">
            <span :class="{ done: todo.done }">{{ todo.text }}</span>
          </div>
          <button @click="removeTodo(todo)" class="button">Hapus</button>
        </li>
      </ul>
      <button @click="hideCompleted = !hideCompleted" class="filter-button">
        {{ hideCompleted ? 'Show all' : 'Hide completed' }}
      </button>
    </div>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container {
  display: flex;
  height: 100vh;
  position: relative;
  justify-content: space-between;
}
.container::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
}
.todo-form, .todo-list {
  background: rgba(255, 255, 255, 0.6);
  border-radius: 15px;
  padding: 20px;
  margin: 20px;
}
.todo-form {
  width: 30%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.todo-form .title {
  font-family: "IBM Plex Mono", monospace;
  font-size: 40px;
  margin-bottom: 20px;
}
.todo-form .input {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 2px solid transparent;
  border-radius: 4px;
  transition: border 0.1s;
}
.todo-form .input:focus {
  border: 2px solid rgb(124, 138, 255);
}
.todo-form .button {
  padding: 10px 20px;
  border: none;
  border-radius: 15px;
  background: #1A1A1A;
  color: #fff;
  cursor: pointer;
  transition: background 0.3s, transform 0.3s;
}
.todo-form .button:hover {
  background: #3B3B3B;
  transform: translateY(-2px);
}
.todo-list {
  width: 60%;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}
.todo-list .header {
  display: flex;
  align-items: center;
  width: 100%;
  background: #000;
  color: #fff;
  padding: 10px;
  border-radius: 15px 15px 0 0;
}
.todo-list .icon {
  width: 50px;
  height: 50px;
}
.todo-list .list-title {
  font-family: "Kanit", sans-serif;
  font-size: 40px;
  margin-left: 10px;
}
.todo-list .list-title span:first-child {
  color: white;
}
.todo-list .list-title span:last-child {
  color: cadetblue;
}
.todo-list .list-items {
  width: 100%;
  padding: 20px;
  overflow-y: auto;
}
.todo-list .list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  margin-bottom: 10px;
  border-bottom: 1px solid #ccc;
}
.todo-list .list-item .checkbox {
  margin-right: 10px;
  transform: scale(1.5);
}
.todo-list .list-item .done {
  text-decoration: line-through;
}
.todo-list .button {
  padding: 5px 10px;
  border: none;
  border-radius: 15px;
  background: #1A1A1A;
  color: #fff;
  cursor: pointer;
  transition: background 0.3s, transform 0.3s;
}
.todo-list .button:hover {
  background: #3B3B3B;
  transform: translateY(-2px);
}
.todo-list .filter-button {
  margin-top: 20px;
  padding: 10px 20px;
  border: none;
  border-radius: 15px;
  background: #1A1A1A;
  color: #fff;
  cursor: pointer;
  transition: background 0.3s, transform 0.3s;
}
.todo-list .filter-button:hover {
  background: #3B3B3B;
  transform: translateY(-2px);
}
</style>
