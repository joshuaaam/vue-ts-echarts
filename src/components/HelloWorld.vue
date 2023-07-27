<script setup lang="ts">
// import { ref } from 'vue'

// import { EChartsOption, init } from 'echarts';

import { onBeforeUnmount, onMounted, ref } from "vue";
import echarts from "../config/echart";

const props = defineProps(["options"]);
const chartRef = ref<HTMLDivElement>();
let chart: echarts.ECharts | null = null;
const resizeHandler = () => {
  chart?.resize();
};
onMounted(() => {
  setTimeout(() => {
    initChart();
  }, 20);
  window.addEventListener("resize", resizeHandler);
});

const initChart = () => {
  chart = echarts.init(chartRef.value as HTMLDivElement);
  chart.setOption({
    ...props.options,
  });
};

onBeforeUnmount(() => {
  window.removeEventListener("resize", resizeHandler);
  chart?.dispose();
});
</script>

<template>
  <div id="chart"  ref="chartRef"></div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
#chart {
  width: 100%;
  height: 100%;
}
</style>
