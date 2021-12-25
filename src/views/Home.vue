<template>
  <div>{{ todaysDate.toDateString() }}</div>
  <day-rater :rating="rating" @ratingChange="updateValue" />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import DayRater from "@/components/DayRater.vue";

export default defineComponent({
  name: "Home",
  data() {
    return {
      rating: 0,
      todaysDate: new Date(),
    };
  },
  components: { DayRater },
  methods: {
    updateValue(newValue: number) {
      this.rating = newValue;
    },
  },
});
</script>
