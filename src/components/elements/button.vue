<template>
  <button 
    @click="$emit('buttonClick')" 
    :class="type">
    {{ label }}
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
      label: String,
      type: String
  }
}
</script>

<style lang="scss" scoped>
.dropdown {
    width: 100%;
}

button {
  cursor: pointer;
}

</style>