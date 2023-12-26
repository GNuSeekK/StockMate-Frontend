<template>
  <div class="chart-wrapper">
    <div class="chart-container" ref="chartContainer">
      <Line :data="chartData" :options="chartOptions"/>
    </div>
  </div>
</template>

<script setup>
import {Chart, registerables} from 'chart.js';
import {Line} from "vue-chartjs";
import {computed} from "vue";
import {useStockStore} from "@/store/stock";
const props = defineProps({
  chartData: Object,
});

Chart.register(...registerables);

const stockStore = useStockStore();
const getStockNameFromCode = stockStore.getStockNameFromCode(props.chartData.stockCode);

const chartOptions = computed(() => {
  return {
    responsive: true,
    maintainAspectRatio: false,
    scales: {
      x: {
        grid: {
          display: false,
        },
        ticks: {
          display: false,
        }
      },
      y: {
        type: 'linear',
        position: 'left',
        grid: {
          display: false,
        },
        ticks: {
          display: true,
        },
      }
    },
    interaction: {
      mode: 'index',
      axis: 'x',
      intersect: false,
    },
    plugins: {
      legend: {
        display: false,
      },
      title: {
        display: true,
        text: getStockNameFromCode,
        font: {
          size: 20,
        }
      },
    },
  }
});
</script>

<style scoped>
.chart-container {
  position: absolute;
  width: 100%;
  height: 100%;
  max-height: 300px;
  padding-left: 10%;
  padding-right: 10%;
}

.chart-wrapper {
  width: 100%;
  position: relative;
  padding-bottom: 20%;
  background-color: white;
}
</style>