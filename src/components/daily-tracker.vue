<template>
  <div class="daily-tracker-container">
    <h1>
    Daily Tracker
    </h1>
    <div class="widget-wrapper">
      <div class="dropdowns-container">
        <Dropdown :options="options" :label="'Duration in bed'"/>
        <Dropdown :options="options" :label="'Duration asleep'"/>
      </div>
      <div class="submit-container">
        <Button :label="'Calculate'"/>
      </div>
    </div>
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
  },
  computed: {
    options(){
      const options = [];
      let hours = 0;
      let min = 30;
      while(hours <= 24){
        if(min === 30){
          if(hours !== 24)options.push(`${hours} hrs. and ${min} min.`)
          min = 0;
          hours ++;
        }
        else{
          options.push(`${hours} hrs.`)
          min = 30;
        }
      }
      return options;
    }
  }
}
</script>

<style lang="scss" scoped>

.widget-wrapper{
  padding: 1rem;

  //tablet landscape
  @media only screen and (min-width: 64rem){
    max-width: 62rem;
    margin: 0 auto;
  }
}

</style>