<template>
  <v-layout class="align-center justify-center" style="height: 100vh;">
  <div style="height: 300px; width: 800px">
    <Bar :data="data" :options="options" />
  </div></v-layout>
</template>

<script lang="ts">
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from "chart.js";
import { Bar } from "vue-chartjs";
import * as chartConfig from "./chartConfig";

ChartJS.register(
  CategoryScale,
  LinearScale,
  BarElement,
  Title,
  Tooltip,
  Legend
);

export default {
  name: "App",
  components: {
    Bar,
  },
  data() {
    return chartConfig;
  }, 
};
</script>