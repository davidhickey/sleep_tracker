<template>
  <div class="dropdown-container">
    <Button 
      @buttonClick="toggle" 
      :label="selection.label ? `${label}: ${selection.label}`: label" 
      :type="'dropdown'"/>
    <Transition name="slide">
    <div v-if="active" class="options-container">
      <ul class="options">
        <li 
          v-for="(option, index) of options" 
          :key="index" class="option"
          @click="handleDropdownSelection(option)"
          :class="{'selected' : option === selection}">
          {{ option.label }}
        </li>
      </ul>
    </div>
    </Transition>
  </div>
</template>

<script>
import Button from './button.vue';

export default {
  name: 'Dropdown',
  components: {
    Button
  },
  props: {
    options: Array,
    label: String,
    name: String
  },
  data(){
    return {
      active: false,
      selection: {
        label: '',
        value: null,
      }
    }
  },
  methods: {
    toggle(){
      this.active = !this.active;
    },
    handleDropdownSelection(option){
      this.selection = this.selection !== option ? option : {label: '', value: null};
      this.$emit('dropdownSelection', {dropdown: this.name, ...this.selection});
    }
  }
}
</script>

<style lang="scss" scoped>
.dropdown-container {
  display: block;
  width: 100%;
  position: relative;

  .options-container {
    position: absolute;
    width: 100%;
    height: 25rem;
    overflow-y: scroll;
    background-color: white;
    z-index: 1;

    .options {
      text-align: left;
      padding-left: .5rem;

      .option {
        list-style-type: none;
        cursor: pointer;

        &.selected {
          background-color: black;
          color: white;
        }

        &:hover{
          background-color: black;
          color: white;
        }
      }
    }
  }
}

.slide-enter-active {
   -moz-transition-duration: 0.3s;
   -webkit-transition-duration: 0.3s;
   -o-transition-duration: 0.3s;
   transition-duration: 0.3s;
   -moz-transition-timing-function: ease-in;
   -webkit-transition-timing-function: ease-in;
   -o-transition-timing-function: ease-in;
   transition-timing-function: ease-in;
}

.slide-leave-active {
   -moz-transition-duration: 0.3s;
   -webkit-transition-duration: 0.3s;
   -o-transition-duration: 0.3s;
   transition-duration: 0.3s;
   -moz-transition-timing-function: cubic-bezier(0, 1, 0.5, 1);
   -webkit-transition-timing-function: cubic-bezier(0, 1, 0.5, 1);
   -o-transition-timing-function: cubic-bezier(0, 1, 0.5, 1);
   transition-timing-function: cubic-bezier(0, 1, 0.5, 1);
}

.slide-enter-to, .slide-leave {
   max-height: 25rem;
   overflow: hidden;
}

.slide-enter, .slide-leave-to {
   overflow: hidden;
   max-height: 0;
}

</style>