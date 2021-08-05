<template>
  <div class="datepicker">
    <input
      class="input"
      v-model="enteredDate"
      @blur="findDate()"
      placeholder="YYYY-MM-DD"
    />
    <table class="datepicker__table">
      <thead>
        <tr>
          <td>
            <button class="btn btn--last" @click="getLastMonth()">&#10094;</button>
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
import { mixin } from "./DatePickerENG.vue";

export default {
  name: "DatePickerRU",
  mixins: [mixin],
  data() {
    return {
      daysOfWeek: ["Пн", "Вт", "Ср", "Чт", "Пт", "Сб", "Вс"],
      monthes: [
        "Январь",
        "Февраль",
        "Март",
        "Апрель",
        "Май",
        "Июнь",
        "Июль",
        "Август",
        "Сентябрь",
        "Октябрь",
        "Ноябрь",
        "Декабрь",
      ],
    };
  },
};
</script>

<style>
</style>