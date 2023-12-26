<template>
  <a-layout-content class="layout-content">
    <div class="welcome-section">
      Welcome to <span class="logo-text">스탁메이트</span>
      <SearchBar />
    </div>
    <div class="content-section">
      <PopularStockSection />
    </div>
    <div class="content-section">
      <NewsSection />
    </div>
  </a-layout-content>
</template>

<script setup>
import SearchBar from '../components/pagecomponent/SearchBar.vue';
import NewsSection from '../components/pagecomponent/NewsSection.vue';
import PopularStockSection from "@/components/pagecomponent/PopularStockSection.vue";
</script>

<style scoped>
.layout-content {
  padding: 50px;
  background-color: white;
}

.welcome-section {
  text-align: center;
  padding-top: 70px;
  border-bottom: 1px double #e8e8e8;
  padding-bottom: 100px;
  font-size: 30px;
  font-weight: bold;
}

.content-section {
  display: flex;
  justify-content: center;
  border-top: 1px double  #e8e8e8;
  padding-top: 50px;
  border-bottom: 1px double #e8e8e8;
  padding-bottom: 50px;
}

.logo-text {
  font-size: 50px;
}
/* 더 필요한 스타일링 추가 */
</style>