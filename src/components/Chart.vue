<template>
  <view class="container" :style="{ height: props.height ?? '300px' }">
    <ec-charts id="mychart-dom-bar" canvasId="mychart-bar" :ec="ecoptions" />
  </view>
</template>
<script lang="ts" setup>
import { ref, watch } from "vue";
import { log } from "@/utils/log";

const echarts = require("../wxcomponents/ec-canvas/echarts");

const props = defineProps<{
  height: string;
  options: any;
}>();

const ecoptions = ref<any>({
  onInit: echartBarInit,
});
const charInfo = ref();

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
  charInfo.value = chart;
  return chart;
}

watch(props.options, (newVal)=>{
  charInfo.value.setOption(newVal)
}, {
  deep: true,
  immediate: true
})
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
