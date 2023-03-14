<template>
  <div>
    <div v-for="(todo) in todos" :key="todo.id" class="todo">
      <span :class="{'checked': todo.done}" @click="$emit('toggleDone', todo.id)" />
      <p :class="{'done': todo.done}">{{ todo.title }}</p>
      <button @click="$emit('editTodo', todo.id)">Modifier</button>
      <button @click="$emit('deleteTodo', todo.id)">Supprimer</button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  todos: Array,
})
  defineEmits(['editTodo', 'deleteTodo', 'toggleDone'])
</script>

<style>
.todo{
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 2em;
  margin: 20px 0;
}
  span{
    width: 10px;
    height: 10px;
    border: 1px solid black;
  }
  .checked::after{
    content: '✓';
    font-weight: bold;
    position: relative;
    top: -9px;
    left: -1px;
  }
  .done {
    text-decoration: line-through;
    color: #777;
  }
</style>
