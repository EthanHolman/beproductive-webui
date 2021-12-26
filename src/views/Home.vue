<template>
  <h1 class="date">{{ todaysDate.toDateString() }}</h1>
  <day-rater :rating="rating" @ratingChange="updateValue" />
  <div class="editorsContainer">
    <accomplishment-editor v-model="accomplishments" />
    <did-not-go-well-editor v-model="didNotGoWell" />
  </div>
  <button @click="save" class="saveButton">Save!</button>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import DayRater from "@/components/DayRater.vue";
import AccomplishmentEditor from "@/components/AccomplishmentEditor.vue";
import DidNotGoWellEditor from "@/components/DidNotGoWellEditor.vue";
import { LOCAL_STORAGE_KEY } from "@/globals";

const formDataModel = {
  rating: 0,
  todaysDate: new Date(),
  accomplishments: [
    "did laundry",
    "robbed a bank",
    "venmo'd my buddy bail money",
  ],
  didNotGoWell: ["went to jail"],
};

export default defineComponent({
  name: "Home",
  data() {
    return { ...formDataModel };
  },
  components: { DayRater, AccomplishmentEditor, DidNotGoWellEditor },
  methods: {
    updateValue(newValue: number) {
      this.rating = newValue;
    },
    save() {
      const formData = { ...this.$data };
      const pastRecords = JSON.parse(
        localStorage.getItem(LOCAL_STORAGE_KEY) ?? "[]"
      );
      localStorage.setItem(
        LOCAL_STORAGE_KEY,
        JSON.stringify([...pastRecords, formData])
      );

      Object.assign(this.$data, { ...formDataModel });
      // this.$data = { ...formDataModel };
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

.save {
  margin: auto;
  display: block;
}
</style>
