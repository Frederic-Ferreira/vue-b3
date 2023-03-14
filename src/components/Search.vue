<template>
    <label for="search-bar">Rechercher un todo ...</label>
    <input type="text" name="search-bar" :value="input" @input="handleChange" />
</template>
  
<script setup>
import { ref, defineEmits, defineProps, watchEffect } from 'vue';

const props = defineProps({
  title: String
});

const input = ref(props.title);

watchEffect(() => {
  input.value = props.title
})

const handleChange = (e) => {
    input.value = e.target.value
    
}

</script>