<template>
  <div class="section-container">
    <div class="section-title">
      <span class="title-text logo-text">인기 종목</span>
      <span class="title-subtext">(오늘의 검색량 상위 3개 종목)</span>
    </div>
    <div class="mini-chart-container">
      <MiniChart v-for="chartData in chartDatas" :key="chartData.code" :chart-data="chartData"/>
    </div>
  </div>
</template>

<script setup>
import {useStockStore} from "@/store/stock"
import {onMounted, ref, watch} from "vue";
import MiniChart from "@/components/chart/MiniChart.vue";

const stockStore = useStockStore();

const chartDatas = ref([]);

watch(() => stockStore.getPopularStockList(), () => {
  const popularStockList = stockStore.getPopularStockList();
  chartDatas.value = popularStockList.map((stock) => {
    return {
      labels: stock['stockPriceDtoList'].map((stockPrice) => stockPrice.date),
      datasets: [
        {
          label: '종가',
          data: stock['stockPriceDtoList'].map((stockPrice) => stockPrice.close),
          borderColor: colorFinder(stock['stockPriceDtoList'][0].close, stock['stockPriceDtoList'][stock['stockPriceDtoList'].length - 1].close),
          backgroundColor: backgroundColorFinder(stock['stockPriceDtoList'][0].close, stock['stockPriceDtoList'][stock['stockPriceDtoList'].length - 1].close),
          fill: true,
          yAxisID: 'y',
        }
      ],
      stockCode: stock['stockCode'],
    };
  });
});

watch(chartDatas, () => {
  console.log(chartDatas.value);
});

const colorFinder = (startDay, today) => {
  if (startDay < today) {
    return '#D32F2F';
  } else if (startDay > today) {
    return '#1976D2';
  } else {
    return '#388E3C';
  }
};

const backgroundColorFinder = (yesterday, today) => {
  if (yesterday < today) {
    return 'rgba(211,47,47,0.3)';
  } else if (yesterday > today) {
    return 'rgba(25,118,210,0.3)';
  } else {
    return 'rgba(56,142,60,0.3)';
  }
};

const loadInitialChartData = async () => {
  await stockStore.loadPopularStockList();
};

onMounted(loadInitialChartData);

</script>

<style scoped>
.mini-chart-container {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.section-title {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 50px;
}

.title-text {
  font-size: 50px;
  font-weight: bold;
  margin-bottom: 10px;
}

.title-subtext {
  font-size: 15px;
  color: #a6a6a6;
}

.section-container {
  width: 100%;
  height: 100%;
}
</style>