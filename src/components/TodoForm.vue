<template>
  <div class="todo-form">
    <form @submit.prevent="mode ? changeTodo() : addNewTodo() ">
      <input type="text" :value="input" @input="event => input = event.target.value" placeholder="Ajouter une tâche">
      <button v-if="!mode" type="submit">Ajouter</button>
      <button @click="changeTodo" v-if="mode" type="submit">Editer</button>
    </form>
  </div>
</template>

<script setup>
import { ref, defineEmits, defineProps, watchEffect } from 'vue';

const emit = defineEmits(['addTodo', 'updateTodo']);

const props = defineProps({
  mode: {
    type: Boolean
  },
  title: String
});

const input = ref(props.title);

watchEffect(() => {
  input.value = props.title
})

const addNewTodo = () => {
  const todo = input.value;
  if (todo) {
    emit('addTodo', todo);
    input.value = '';
  }
};

const changeTodo = () => {
  const title = input.value;
  if(title){
    emit('updateTodo', title);
    input.value = '';
  }
};
</script>

<style>
.todo-form{
  background-color: rgb(165, 165, 165);
  border-radius: 5px;
  padding: 10px 20px;
}

.todo-form input{
  height: 33px;
  border-radius: 2px;
  border: none;
  padding-left: 5px;
}
.todo-form button{
  margin-left: 20px;
}
</style>