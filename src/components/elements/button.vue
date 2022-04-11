<template>
  <button 
    @click="$emit('buttonClick')" 
    :class="[state, type]"
    :disabled="disabled"
    >
    {{ label }}
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    label: String,
    type: String,
    state: String,
    disabled: {
      default: false,
      type: Boolean
    },
  }
}
</script>

<style lang="scss" scoped>

button {
  cursor: pointer;
  border: 1px solid #0a1153;
  color: #0a1153;
  background-color: white;
  height: 3rem;
  font-size: 16px;
  border-radius: .5rem;

  &.dropdown {
    width: 100%;
  }

  &.selected {
    background-color: #0a1153;
    color: white;
  }

  &.disabled {
    background-color: grey;
  }

  &:hover:not(.disabled) {
    opacity: .8;
  }
}

</style>