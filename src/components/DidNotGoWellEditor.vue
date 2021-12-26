<template>
  <div>
    <h2>What didn't go well today?</h2>
    <textarea v-model="value" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: ["modelValue"],
  emits: ["update:modelValue"],
  computed: {
    value: {
      get() {
        return this.modelValue.join("\n");
      },
      set(newVal: string) {
        this.$emit("update:modelValue", newVal.split("\n"));
      },
    },
  },
});
</script>

<style scoped>
textarea {
  width: 100%;
  height: 9rem;
  display: block;
}
</style>
