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
          :disabled="!canSubmit"
          @buttonClick="onSubmit"/>
      </div>
      <div class="score-results-container">
        <span v-if="apiStatus.status === 'success'">
          Your sleep score is 
          <b class="sleep-score">
            {{this.calculateScore()}}
          </b>
          !
        </span>
        <span v-else-if="apiStatus.status === 'error'" class="error">
          {{ apiStatus.text }}
        </span>
        <span v-else>
          {{ apiStatus.text }}
        </span>
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
      duration_in_bed: null,
      duration_asleep: null,
      showScore: false,
      apiStatus: {
        text: '',
        status: ''
      },
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
      return this.duration_in_bed && this.duration_asleep;
    }
  },
  methods: {
    handleDropdownSelection(selection){
      if(selection.dropdown === "bed"){
        this.duration_in_bed = selection.value
      }
      else{
        this.duration_asleep = selection.value;
      }
    },
    calculateScore(){
      return Math.round(100 * (this.duration_asleep / this.duration_in_bed));
    },
    onSubmit(){
      this.scoreOutputText = this.calculateScore();
      this.apiStatus = {
        text: 'Loading',
        status: 'loading'
      };
      this.postData();
    },
    async postData(){
      const url = `https://6254587289f28cf72b5c4e25.mockapi.io/api/staging/sleep_score/`
      const res = await fetch(url, {
        method: 'POST',
        body: JSON.stringify({
          id: 1,
          score: this.calculateScore()
        })
      });

      if(!res.ok){
        console.error('API failed ', res);
        // TODO: remove setTimeout after demo
        setTimeout(() => {
          this.apiStatus = {
            text:'Failed to save Sleep Score. Please try again later.',
            status: 'error',
          }
          this.showScore = false;
        }, 2000);
        return null
      }
      else {
        const data = await res.json();    
        // TODO: remove setTimeout after demo
        setTimeout(() => {
          this.apiStatus = {
            text: '',
            status: 'success'
          };
          this.showScore = true;
        }, 2000);
        return data;
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