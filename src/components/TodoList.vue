<script setup>
import { ref } from "vue";

const todoName = ref("");
const todos = ref([]);

function addTodo() {
  todos.value.push({
    title: todoName.value,
    complete: false,
  });
  todoName.value = "";
}

function markAsDone(todoIndex) {
  todos.value.map((todo, index) => {
    if (index === todoIndex) {
      todo.complete = !todo.complete;
    }
    return todo;
  });
}
function deleteItem(todo) {
  todos.value = todos.value.filter((t) => t != todo);
}
</script>

<template>
  <div>
    <input v-model="todoName" placeholder="Type here.." />
    <button @click="addTodo">Add todo</button>
  </div>

  <ul>
    <li v-for="(todo, index) in todos" :key="index">
      <span :class="{ completed: todo.complete }">
        {{ todo.title }}  <button @click="markAsDone(index)">✓</button>
      
      </span>
     <button @click="deleteItem(todo)">x</button>
    </li>
  </ul>
</template>

<style>
* {
  list-style-type: none;
  }

ul {
  display: flex;
  text-align: center ;
  justify-content: space-between;
  flex-direction: column;
  }
li {
  padding: 10px;
  margin-right: 14px;
}
span {
  padding: 10px;
}

.completed {
 opacity: 30%;
 font-weight: bold;
 text-decoration: line-through;
 color: rgb(251, 127, 255);
}
</style>
