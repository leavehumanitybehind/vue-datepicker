<template>
  <div class="datepicker">
    <input class="input" v-model="enteredDate" @blur="findDate()" placeholder="YYYY-MM-DD"/> 
    <table class="datepicker__table">
      <thead>
        <tr>
          <td>
            <button class="btn btn--last" @click="getLastMonth()">&#10094;
</button>
          </td>
          <td colspan="5">{{ monthes[currMonth] }} {{ currYear }}</td>
          <td>
            <button class="btn btn--next" @click="getNextMonth()">&#10095;</button>
          </td>
        </tr>
        <tr>
          <td
            class="week"
            v-for="(day, index) in daysOfWeek"
            :key="day + index"
          >
            {{ day }}
          </td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(week, index) in getDays()" :key="week + index">
          <td
            v-for="(day, index) in week"
            :key="day + index"
            @click="getDay(day.index)"
            class="days"
            :class="{
              isCurrent: day.index === currDay,
              isSelected: day.index === selected,
            }"
            :style="{ color: day.weekend }"
          >
            {{ day.index }}
          </td>
        </tr>
      </tbody>
    </table>
    <p class="selected__info" v-show="selectedDay">
      {{ currYear }} {{ monthes[currMonth] }} {{ selectedDay }}
    </p>
  </div>
</template>

<script>
export let mixin = {
  data() {
    return {
      enteredDate: "",
      selected: "",
      selectedDay: "",
      currDay: new Date().getDate(),
      currMonth: new Date().getMonth(),
      currYear: new Date().getFullYear(),
    };
  },
  methods: {
    getDays() {
      let firstMonthDay = "1";
      let lastMonthDay = new Date(
        this.currYear,
        this.currMonth + 1,
        0
      ).getDate();
      let week = 0;
      let days = [];
      days[week] = [];
      let weekendColor = "#ff0000";

      for (let i = 1; i <= lastMonthDay; i++) {
        let currentDay = new Date(this.currYear, this.currMonth, i).getDay();
        if (currentDay != firstMonthDay) {
          let d = { index: i };
          days[week].push(d);
          currentDay == 6 || currentDay == 0 ? (d.weekend = weekendColor) : "";
        } else {
          week++;
          days[week] = [];
          let d = { index: i };
          days[week].push(d);
        }
      }
      if (days[0].length > 0) {
        for (let i = days[0].length; i < 7; i++) {
          days[0].unshift("");
        }
      }
      return days;
    },
    getLastMonth() {
      this.currMonth--;
      if (this.currMonth < 0) {
        this.currMonth = 12;
        this.currMonth--;
        this.currYear--;
      }
    },
    getNextMonth() {
      this.currMonth++;
      if (this.currMonth > 11) {
        this.currMonth = -1;
        this.currMonth++;
        this.currYear++;
      }
    },
    getDay(i) {
      this.selected = i;
      this.selectedDay = event.target.innerHTML;
    },
    findDate() {
      if (this.enteredDate.length === 10) {
        let year = this.enteredDate.substring(0,4);
      let month = this.enteredDate.substring(5,7);
      let day = this.enteredDate.substring(8,10);
      month >= 10? '' : month = this.enteredDate.substring(6,7);
      day >= 10 ? '' : this.enteredDate.substring(9,10);
      this.currYear = year;
      this.currMonth = month-1;
      this.currDay = new Date(this.currYear, this.currMonth, day).getDate();
      }
      this.enteredDate = ''
      
    }
  },
};
export default {
  name: "DatePickerENG",
  mixins: [mixin],
  data() {
    return {
      daysOfWeek: ["Mn", "Tu", "We", "Th", "Fr", "Sa", "Su"],
      monthes: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ],
    };
  },
};
</script>

<style>
.datepicker__table {
  margin: 0 auto;
  width: 30%;
  text-align: center;
  border-collapse: collapse;
}

button {
  cursor: pointer;
  border: none;
  background-color: inherit;
}


.btn:hover{
color: grey;
}

.input {
  width: 100%;
  margin: 10% 0;
  padding: 3% 1% 3% 2%;

}

.week {
  background-color: rgba(0, 0, 0, 0.1);
}

.isSelected {
  background-color: yellow;
}

.isCurrent {
  background-color: violet;
}

.selected__info {
  text-align: center;
  background-color: rgba(0, 0, 0, 0.1);
}
td {
  padding: 10px;
}
.days {
  cursor: pointer;
}
.days:hover {
  opacity: 0.6;
}
</style>