<template>
  <button @click="clearDone">Effacer les tâches accomplies</button>
</template>

<script>
export default {
  name: 'ClearDone',
  methods: {
    clearDone() {
      this.$emit('clear-done')
    }
  }
}
</script>
