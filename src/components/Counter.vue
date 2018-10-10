<template>
  <div id="container">
    <div id="header">
      Days to end of year
    </div>
    <div id="counter">
      <span id="days-remaining">{{daysRemaining}}</span> days left from today: {{currentDate  }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Counter',
  data: function() {
    return {
      ordinalOperators: ["st", "nd", "rd", "th"],
      monthArray: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
      daysRemaining: 0
    }
  },
  computed: {
    currentDate() {
      let currentDate = new Date();
      return `${this.monthArray[currentDate.getMonth()]} ${this.calculateOrdinalOperator(currentDate.getDate())} ${currentDate.getFullYear()}`
    }
  },
  methods: {
    calculateOrdinalOperator(date) {
      let ordinal = undefined;
      switch(date) {
        case 1:
          orginal = "st"
          break;
        case 2: 
          orginal = "nd"
          break;
        case 3:
          ordinal = "rd"
          break;
        default:
          ordinal = "th"
          break;
      }
      return `${date}${ordinal}`;
    },
    calculateDaysRemaining() {
      let totalSecondsInDay = 60 * 60 * 24 * 1000;
      let lastDayOfYear = new Date(new Date().getFullYear(), 11, 31);
      let daysRemaining = Math.round((lastDayOfYear.getTime() - (new Date().getTime())) / totalSecondsInDay);
      this.daysRemaining = daysRemaining;
    }
  },
  mounted() {
    this.calculateDaysRemaining();
  }
}
</script>
<style>
  * {
    background-color: #A0CFEC;
    font-family: "Whitney Cond A", "Whitney Cond B", "Lato", "Lucida Grande", "Lucida Sans Unicode", Tahoma, Sans-Serif
  }
  #container {
    display: grid;
    justify-items: center;
    align-items: center;
    grid-template-columns: repeat(3, 33%);
    grid-template-rows: 40px 50px 40px;
  }
  #counter {
    grid-column-start: 2;
    grid-column-end: 3;
    grid-row-start: 2;
    grid-row-end: 3;
  }
  #header {
    width: 400px;
    text-align: center;
    line-height: 36px;
    background-color: white;
    border-radius: 100%;
    grid-column-start: 1;
    grid-column-end: 4;
  }
  #days-remaining {
    color: darkred;
  }
</style>
