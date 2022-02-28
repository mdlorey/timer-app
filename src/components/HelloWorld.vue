<template>
  <div class="hello">
    <h2>Timer Application</h2>
    <label>Input a Date to count to</label><br />
    <input type="text" v-model="dateInput" placeholder="mm/dd/yyyy hh:mm" /><br />
    <button @click="countdown()">Count Up/Down</button>
    <p>
      {{ timerDisplay }}
    </p>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      timerDisplay: null,
      dateInput: '03/01/2022 14:46',
      // dateInput: '02/27/2022 14:46',
      countdownInterval: null
    }
  },
  mounted() {
    // this.countdown(10);

    // console.log(this.formatDate(new Date()));
  },
  methods: {
    formatDate(value) {
      if (value) {
        return moment(String(value)).format('MM/DD/YYYY');
      }
    },
    calculateDuration() {
      // console.log(new Date(this.dateInput));
      const now = moment(new Date());
      const then = moment(new Date(this.dateInput));
      return now.diff(then, 'seconds');
      // console.log(now.diff())
    },
    // plain date and text time input
    // count up or down from time provided

    // mm/dd/yyy - hh:mm
    countdown() {
      let duration = Math.abs(this.calculateDuration());

      let timer = duration, minutes, seconds;
      this.clearTheInterval();
      this.countdownInterval = setInterval(() => {
        minutes = parseInt(timer / 60, 10);
        seconds = parseInt(timer % 60, 10);

        minutes = minutes < 10 ? '0' + minutes : minutes;
        seconds = seconds < 10 ? '0' + seconds : seconds;

        this.timerDisplay = `${minutes}:${seconds}`;
        if (--timer < 0) {
          timer = duration;
        }
      }, 1000);
    },
    clearTheInterval() {
      clearInterval(this.countdownInterval);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
