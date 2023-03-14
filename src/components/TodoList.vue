<template>
  <div>
    <div v-for="(todo, index) in todos" :key="index" class="todo">
      <span :class="{'checked': todo.done}" @click="$emit('toggleDone', index)" />
      <p :class="{'done': todo.done}">{{ todo.title }}</p>
      <button @click="$emit('editTodo', index)">Modifier</button>
      <button @click="$emit('deleteTodo', index)">Supprimer</button>
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
