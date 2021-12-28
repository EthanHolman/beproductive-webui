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
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { format } from "date-fns";

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

  return buildWeeksDaysStructure(allDates);
}

export default defineComponent({
  data() {
    return {
      dates: getDates(),
    };
  },
  methods: {
    formatWeek(dates: Date[]): string {
      if (!dates || dates.length === 0) return "";

      const filteredDates = dates.filter((x) => !!x);

      const formatter = (date: Date) => format(date, "MMM d");
      return (
        formatter(filteredDates[0]) +
        " - " +
        formatter(filteredDates[filteredDates.length - 1])
      );
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
