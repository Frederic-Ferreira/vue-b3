<template>
  <button id="clear-all" @click="$emit('clearAll')">Effacer tout</button>
</template>

<script setup>
  defineEmits(['clearAll'])
</script>

<style>
#clear-all{
  margin-top: 20px;
  background-color: red;
  color: white;
}
</style>