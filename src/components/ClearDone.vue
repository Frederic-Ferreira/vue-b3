<template>
  <button id="clear-done" @click="$emit('clearDone')">Effacer les tâches accomplies</button>
</template>

<script setup>
  defineEmits(['clearDone'])
</script>

<style>
#clear-done{
  background-color: black;
  color: white;
  margin-left: 20px;
  margin-top: 20px;
}
</style>