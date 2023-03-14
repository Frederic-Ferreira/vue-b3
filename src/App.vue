<template>
  <div>
    <h1>Ma Todo List</h1>
    <TodoForm :mode="editing" @addTodo="addTodo" @updateTodo="updateTodo" :title="title" />
    <TodoList :todos="todos" @editTodo="editTodo" @deleteTodo="deleteTodo" @toggleDone="toggleDone" />
    <button @click="clearAll">Effacer tout</button>
    <button @click="clearDone">Effacer les tâches accomplies</button>
    <p>Vous avez {{ remainingTodos }} tâche(s) restantes!</p>
  </div>
</template>

<script setup>
import { ref, watchEffect } from 'vue';
import TodoForm from './components/TodoForm.vue';
import TodoList from './components/TodoList.vue';

const todos = ref([]);

const title = ref('');

const editing = ref(false);

const editingIndex = ref(null);

const remainingTodos = ref(0);

watchEffect(() => {
  remainingTodos.value = todos.value.filter(todo => todo.done !== true).length
})

const addTodo = (input) => {
  if (input !== '') {
    todos.value.push({
      title: input,
      done: false,
    });
  }
};

const updateTodo = (title) => {
  todos.value[editingIndex.value].title = title
  editing.value = false
}

const editTodo = (index) => {
  editing.value = true
  title.value = todos.value[index].title
  editingIndex.value = index
};

const deleteTodo = (index) => {
  todos.value.splice(index, 1)
};

const clearAll = () => {
  todos.value = []
};

const clearDone = () => {
  todos.value = todos.value.filter((todo) => !todo.done);
};

const toggleDone = (index) => {
  todos.value[index].done = !todos.value[index].done;
};

</script>

