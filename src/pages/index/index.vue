<template>
  <view>
    <CommChart :height="chartHeight.one" :options="chartOptions.one" />
  </view>
</template>
<script lang="ts" setup>
import { ref, onMounted } from "vue";
import CommChart from "@/components/Chart.vue";

const chartHeight = ref({
  one: "300px",
});
const chartOptions = ref<{
  one: any;
}>({
  one: {
    tooltip: {
      trigger: "item",
    },
    legend: {
      top: "5%",
      left: "center",
    },
    series: [
      {
        name: "Access From",
        type: "pie",
        radius: ["40%", "70%"],
        avoidLabelOverlap: false,
        itemStyle: {
          borderRadius: 10,
          borderColor: "#fff",
          borderWidth: 2,
        },
        label: {
          show: false,
          position: "center",
        },
        emphasis: {
          label: {
            show: true,
            fontSize: "40",
            fontWeight: "bold",
          },
        },
        labelLine: {
          show: false,
        },
        data: [
          { value: 1048, name: "Search Engine" },
          { value: 735, name: "Direct" },
          { value: 580, name: "Email" },
          { value: 484, name: "Union Ads" },
          { value: 300, name: "Video Ads" },
        ],
      },
    ],
  },
});

function initData() {
  setInterval(()=>{
    console.log("执行了1000")
    const value = Math.floor(Math.random() * 100)
    chartOptions.value.one.series[0].data = [{ value, name: "Search Engine -> " + value }];
  }, 2000)
}

onMounted(()=>{
  initData()
})
</script>
<style scoped lang="scss"></style>
