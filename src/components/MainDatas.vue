<template>
  <div>
    <div><strong> Bateria: </strong>{{ item["bateria"] }}%</div>
    <div><strong> Temperatura: </strong>{{ item["temperatura"] }}</div>
    <div>
      <strong> Georreferência: </strong
      >{{ item["payload"][0]["georeferencia"] }}
    </div>
    <div>
      <strong> Magnetometro: </strong>
      {{ calculaMag(item["payload"][0]["magnetometro"]) }} |
      {{ item["payload"][0]["magnetometro"] }}
    </div>
    <div><strong> Data: </strong> {{ item["data"] }}</div>
  </div>
</template>

<script>
import { defineComponent, PropType } from "vue";

export default defineComponent({
  props: ["item"],
  methods: {
    calculaMag(mag) {
      let sum = 0;
      mag.forEach((element) => {
        sum += element * element;
      });
      return Math.sqrt(sum).toFixed(3);
    },
  },
});
</script>

<style></style>
