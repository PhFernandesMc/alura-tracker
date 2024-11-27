<template>
  <button class="button" @click="clickEvent" :disabled="!buttonState">
    <span class="icon">
      <component :is="icon" />
    </span>
    <span>{{ text }}</span>
  </button>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import type { FunctionalComponent } from "vue";

export default defineComponent({
  name: "Button",
  props: {
    text: {
      type: String as PropType<string>,
      default: "click me",
    },
    clickEvent: {
      type: Function as PropType<() => void>,
      required: true,
    },
    buttonState: {
      type: Boolean,
      default: true,
    },
    icon: {
      type: Function as PropType<FunctionalComponent>,
      required: true,
    },
  },
});
</script>

<style scoped></style>

