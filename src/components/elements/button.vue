<template>
  <button 
    @click="$emit('buttonClick')" 
    :class="type"
    :disabled="disabled">
    {{ label }}
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    label: String,
    type: String,
    disabled: {
      default: false,
      type: Boolean
    },
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