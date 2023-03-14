<template>
  <div class="home">
    <h1>Ma Todo List</h1>
    <div class="search-bar">
      <label id="label-search" for="search">Rechercher un todo ...</label>
      <input type="text" name="search" v-model="searchValue" />
    </div>
    <TodoForm :mode="editing" @addTodo="addTodo" @updateTodo="updateTodo" :title="title" />
    <TodoList :todos="displayedTodos" @editTodo="editTodo" @deleteTodo="deleteTodo" @toggleDone="toggleDone" />
    <ClearAll @clearAll="clearAll" />
    <ClearDone @clearDone="clearDone" />
    <p id="remaining-todos">Vous avez {{ remainingTodos }} tâche(s) restantes!</p>
  </div>
</template>

<script setup>
import { ref, watchEffect } from 'vue';
import TodoForm from './components/TodoForm.vue';
import TodoList from './components/TodoList.vue';
import ClearAll from './components/ClearAll.vue';
import ClearDone from './components/ClearDone.vue'

const searchValue = ref('');

const todos = ref([]);

const displayedTodos = ref([])

const title = ref('');

const editing = ref(false);

const editingId = ref(null);

const remainingTodos = ref(0);

watchEffect(() => {
  displayedTodos.value = todos.value.filter(todo => todo.title.includes(searchValue.value))
  remainingTodos.value = displayedTodos.value.filter(todo => todo.done !== true).length
})

const addTodo = (input) => {
  if (input !== '') {
    todos.value.push({
      id: Date.now(), 
      title: input,
      done: false,
    });
  }
};

const updateTodo = (title) => {
  todos.value.find(todo => todo.id === editingId.value).title = title
  editing.value = false
}

const editTodo = (id) => {
  editing.value = true
  title.value = todos.value.find(todo => todo.id === id).title
  editingId.value = id
};

const deleteTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id)

};

const clearAll = () => {
  todos.value = []
};

const clearDone = () => {
  todos.value = todos.value.filter((todo) => !todo.done);
};

const toggleDone = (id) => {
  todos.value.find(todo => todo.id === id).done = !todos.value.find(todo => todo.id === id).done;
};

</script>

<style>

#remaining-todos{
margin-top: 33px;
}

.search-bar{
  margin-bottom: 33Px;
  padding-bottom: 10px;
  border-bottom: 2px solid black;
}

#label-search{
  margin-right: 10px;
}
</style>
