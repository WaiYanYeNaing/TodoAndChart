<template>
  <v-layout class="align-center justify-center" style="height: 100vh;">
  <div :style="`position: relative; width: 1000px`">  
    <img v-for="(v, i) of data.datasets[0].data" :key="i" :src="`https://picsum.photos/seed/${Math.random()}/30/30`" alt="logo" width="30" :style="`position: absolute; bottom: ${(v * 5.25) + 50}px; left: ${53 + (i * 81)}px; border-radius: 100px; ${barWidth < 1000 && 'display: none;'}`">
    <Bar :data="data" :options="options" id="bar"/>
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
    return {...chartConfig, barWidth: 0};
  }, 
  mounted() {
    this.getWdithOfBar()
  },
  methods: {
    getWdithOfBar() {
      console.log(document.getElementById('bar')?.clientWidth)
      this.barWidth = document.getElementById('bar')?.clientWidth
    }
  } 
};
</script>