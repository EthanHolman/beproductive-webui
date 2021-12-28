<template>
  <h1>Calendar!</h1>
  <table>
    <thead>
      <tr>
        <th></th>
        <th>Sun</th>
        <th>Mon</th>
        <th>Tues</th>
        <th>Wed</th>
        <th>Thur</th>
        <th>Fri</th>
        <th>Sat</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(week, weekIndex) in dates" :key="weekIndex">
        <td>{{ formatWeek(week) }}</td>
        <td v-for="(day, dayIndex) in week" :key="dayIndex">
          {{ day ? day.getDate() : "" }}
        </td>
      </tr>
    </tbody>
  </table>
  <div>{{ numRows }}</div>
  <button @click="doDebug">Do Debug</button>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";

function buildWeeksDaysStructure(dates: any) {
  const arr = [];
  let weekArr = [];

  while (dates.length > 0) {
    const remove = dates.splice(0, 1)[0];
    weekArr.push(remove);

    if (weekArr.length === 7) {
      weekArr.reverse();
      arr.push(weekArr);
      weekArr = [];
    }
  }

  return arr;
}

function getDates() {
  const dates = [];

  const day = new Date();

  while (dates.length < 30) {
    dates.push(new Date(day.getTime()));
    day.setDate(day.getDate() - 1);
  }

  const numBlanksToAdd = 5 - dates[dates.length - 1].getDay();
  const blanks = [...Array(numBlanksToAdd).keys()].map((x) => undefined);

  const allDates = [...blanks, ...dates];

  return reactive(buildWeeksDaysStructure(allDates));
}

export default defineComponent({
  data() {
    return {
      dates: getDates(),
      stuff: { mything: "asdf" },
    };
  },
  methods: {
    doDebug() {
      console.log(this.$data.dates);
    },
    doDebug2(stuff: any) {
      console.log(stuff);
    },
    formatWeek(dates: Date[]): string {
      // return "asdf";
      if (!dates || dates.length === 0) return "";
      const filteredDates = dates.filter((x) => !!x);
      return (
        "" +
        filteredDates[0].getDate() +
        " - " +
        filteredDates[filteredDates.length - 1].getDate()
      );
    },
  },
  computed: {
    numRows() {
      const val = Math.ceil(this.dates.length / 7);
      return val;
    },
  },
});
</script>

<style scoped>
table {
  border-collapse: collapse;
}

table,
th,
td {
  border: 1px solid black;
}
</style>
