<template>
  <div class="rater">
    <button
      v-for="num in 5"
      :key="num"
      @click="handleClick(num)"
      class="button"
      :class="{ selected: rating >= num }"
    >
      {{ num }}
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  emits: ["ratingChange"],
  props: {
    rating: Number,
  },
  methods: {
    handleClick(rating: number) {
      this.$emit("ratingChange", rating);
    },
  },
});
</script>

<style scoped>
.rater {
  margin: auto;
  display: flex;
  justify-content: center;
}
.button {
  background-color: #d0d0d0;
  border: 1px solid #999;
  border-radius: 5px;
  padding: 1rem;
  margin: 1rem;
}
.selected {
  background-color: green;
}
</style>
