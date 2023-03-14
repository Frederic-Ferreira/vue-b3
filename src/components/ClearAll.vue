<template>
  <button @click="clearAll">Effacer tout</button>
</template>

<script>
export default {
  name: 'ClearAll',
  methods: {
    clearAll() {
      this.$emit('clear-all')
    }
  }
}
</script>
