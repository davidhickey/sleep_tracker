<template>
  <div class="daily-tracker-container">
    <h1>
    Daily Sleep Tracker
    </h1>
    <div class="widget-wrapper">
      <div class="dropdowns-container">
        <Dropdown
          @dropdownSelection="handleDropdownSelection"
          :options="options" 
          :label="'Duration in bed'"
          :name="'bed'"
        />
        <Dropdown
          @dropdownSelection="handleDropdownSelection"
          :options="options" 
          :label="'Duration asleep'"
          :name="'sleep'"
        />
      </div>
      <div class="submit-container">
        <Button 
          :label="'Calculate'" 
          :disabled="!canSubmit"/>
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
  data(){
    return {
      bedDataSelection: null,
      sleepDataSelection: null,
    }
  },
  computed: {
    options(){
      const options = [];
      let hours = 0;
      let min = 30;
      while(hours <= 24){
        const value = hours + (min === 30 ? 0.5 : 0);
        if(min === 30){
          if(hours !== 24)options.push({
            label: `${hours} hrs. and ${min} min.`,
            value
          });
          min = 0;
          hours ++;
        }
        else{
          options.push({
            label:`${hours} hrs.`,
            value
          });
          min = 30;
        }
      }
      return options;
    },
    canSubmit(){
      return this.bedDataSelection && this.sleepDataSelection;
    }
  },
  methods: {
    handleDropdownSelection(selection){
      if(selection.dropdown === "bed"){
        this.bedDataSelection = selection.value
      }
      else{
        this.sleepDataSelection = selection.value;
      }
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