<template>
  <h1 class="date">{{ todaysDate.toDateString() }}</h1>
  <day-rater :rating="rating" @ratingChange="updateValue" />
  <div class="editorsContainer">
    <accomplishment-editor v-model="accomplishments" />
    <did-not-go-well-editor v-model="didNotGoWell" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import DayRater from "@/components/DayRater.vue";
import AccomplishmentEditor from "@/components/AccomplishmentEditor.vue";
import DidNotGoWellEditor from "@/components/DidNotGoWellEditor.vue";

export default defineComponent({
  name: "Home",
  data() {
    return {
      rating: 0,
      todaysDate: new Date(),
      accomplishments: [
        "did laundry",
        "robbed a bank",
        "venmo'd my buddy bail money",
      ],
      didNotGoWell: ["went to jail"],
    };
  },
  components: { DayRater, AccomplishmentEditor, DidNotGoWellEditor },
  methods: {
    updateValue(newValue: number) {
      this.rating = newValue;
    },
  },
});
</script>

<style scoped>
.date {
  text-align: center;
}

.editorsContainer {
  margin: auto;
  width: 80%;
}
</style>
