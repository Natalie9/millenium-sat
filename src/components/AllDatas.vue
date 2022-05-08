<template>
  <div>
    <div v-for="value in Object.keys(item)" :key="value">
      {{ value }} {{ item[value] }}
    </div>
  </div>
</template>

<script>
import { defineComponent, PropType } from "vue";

export default defineComponent({
  props: ["item"],
});
</script>

<style></style>
