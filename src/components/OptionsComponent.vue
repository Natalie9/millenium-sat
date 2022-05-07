<template>
  <div>
    <h4 style="display: inline; margin: 3em 0px">
      Próxima atualização: {{ todoCount }}
    </h4>
    <button @click="getData" style="display: inline; margin: 3em">
      Atualizar
    </button>
    <p v-if="isLoading">carregando ...</p>
    <ol>
      <li
        v-for="item in lista"
        :key="item['_id']"
        style="border: 1px black solid; padding: 2em"
      >
        <div v-for="value in Object.keys(item)" :key="value">
          {{ value }} {{ item[value] }}
        </div>
      </li>
    </ol>
  </div>
</template>

<script lang="ts">
import Plotly from "plotly.js";

import { defineComponent, PropType } from "vue";
import axios from "axios";
const fourMinutes = 60 * 4;
export default defineComponent({
  name: "OptionsComponent",
  data(): {
    clickCount: number;
    lista: Array<any>;
    count: number;
    isLoading: boolean;
  } {
    return {
      clickCount: 0,
      lista: [],
      count: fourMinutes,
      isLoading: false,
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    increment(): void {
      this.clickCount += 1;
    },
    async getData() {
      this.isLoading = true;
      const response = await axios.get(
        "https://pkg-receiver-millenium.vercel.app/api/getData/1"
      );
      const lista = response.data.lista;
      const visu = lista.reduce((arr: any, value: any) => {
        arr.push(JSON.parse(value.replace("\\", "")));
        return arr;
      }, []);
      this.isLoading = false;
      this.lista = [...visu.slice(-5)];
    },
  },
  computed: {
    todoCount(): string {
      window.setTimeout(() => this.count--, 1000);
      if (this.count <= 0) {
        this.count = fourMinutes;
        this.getData();
      }
      const minute = parseInt(this.count / 60 + "");
      let seconds = parseInt((this.count % 60) + "");

      return "0" + minute + ":" + (seconds < 10 ? "0" + seconds : seconds);
    },
  },
});
</script>
