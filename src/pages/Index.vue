<template>
  <q-page class="row items-center justify-evenly">
    <example-component></example-component>
  </q-page>
</template>

<script lang="ts">
import ExampleComponent from "components/OptionsComponent.vue";
import { defineComponent } from "vue";

export default defineComponent({
  name: "PageIndex",
  components: { ExampleComponent },
  data() {},
});
</script>
