<template>
  <div>
    <h1>
    Daily Tracker
    </h1>
    <Dropdown />
    <Dropdown />
    <Button />
  </div>
</template>

<script>
import Dropdown from './elements/dropdown.vue';
import Button from './elements/button.vue';

export default {
  name: 'DailyTracker',
  components: {
    Dropdown,
    Button
  }
}
</script>

<style lang="scss" scoped>

</style>