<template>
  <view class="container" :style="{ height: props.height ?? '300px' }">
    <ec-charts id="mychart-dom-bar" canvasId="mychart-bar" :ec="ecoptions" />
  </view>
</template>
<script lang="ts" setup>
import { ref } from "vue";
import { log } from "@/utils/log";
import { IEChartOption } from "../models";

const echarts = require("../wxcomponents/ec-canvas/echarts");

const props = defineProps<{
  height: string;
  options: IEChartOption;
}>();

const ecoptions = ref<any>({
  onInit: echartBarInit,
});

function echartBarInit(
  canvas: any,
  width: number,
  height: number,
  dpr: number
) {
  log.d(canvas, "canvas");
  log.d(echarts, "echarts");
  const chart = echarts.init(canvas, null, {
    width,
    height,
    devicePixelRatio: dpr, // 像素
  });
  log.d(props.options, "props.options");

  chart.setOption(props.options ?? {});
  canvas.setChart(chart);
  return chart;
}
</script>
<style scoped lang="scss">
.container {
  width: 100%;
}
.mychart-bar {
  width: 100%;
  height: 100%;
}
</style>
