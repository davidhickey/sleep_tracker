<template>
  <div class="dropdown-container">
    <Button @buttonClick="toggle" :label="label" :type="'dropdown'"/>
    <Transition name="slide">
    <div v-if="active" class="options-container">
      <ul class="options">
        <li v-for="(option, index) of options" :key="index" class="option">
          {{ option }}
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
  },
  data(){
    return {
      active: false
    }
  },
  methods: {
    toggle(){
      this.active = !this.active;
    }
  }
}
</script>

<style lang="scss" scoped>
.dropdown-container {
  display: inline-block;
  width: 50%;
  position: relative;

  .options-container {
    position: absolute;
    width: 100%;
    height: 25rem;
    overflow-y: scroll;
    background-color: white;

    .options {
      text-align: left;
      padding-left: .5rem;

      .option {
        list-style-type: none;
        cursor: pointer;

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