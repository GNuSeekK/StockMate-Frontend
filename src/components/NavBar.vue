<template>
  <a-layout id="components-layout">
    <div class="nav-right">
      <a-button class="signup-button" @click="moveToJoinForm"> 회원가입</a-button>
      <a-button class="login-button" @click="showLoginModal">로그인</a-button>
    </div>
    <a-layout-header id="header">
      <div class="header-container">
        <img src="@/assets/img/logo.png" alt="logo" width="80" height="80" @click="redirectToHome">
        <a class="logo-text" @click="redirectToHome">스탁메이트</a>
      </div>
      <div class="menu-container">
        <ul
            class="menu"
        >
          <li :class="{ selected: selectedKey === 'news' }" @click="selectMenu('news')">
            <router-link to="/news">뉴스</router-link>
          </li>
          <li :class="{ selected: selectedKey === 'stock-today' }" @click="selectMenu('stock-today')">
            <router-link to="/stock-today">오늘의 주식</router-link>
          </li>
          <li :class="{ selected: selectedKey === 'chart' }" @click="selectMenu('chart')">
            <router-link to="/chart">주식 차트</router-link>
          </li>
          <li :class="{ selected: selectedKey === 'mychart' }" @click="selectMenu('mychart')">
            <router-link to="/mychart">나만의 차트</router-link>
          </li>
          <li :class="{ selected: selectedKey === 'mypage' }" @click="selectMenu('mypage')">
            <router-link to="/mypage">마이페이지</router-link>
          </li>
        </ul>
      </div>
    </a-layout-header>
  </a-layout>
</template>

<script setup>
import router from "@/router";
import {ref} from "vue";

const selectedKey = ref('home');
const redirectToHome = () => {
  router.push('/');
  selectedKey.value = 'home';
};
const selectMenu = (key) => {
  selectedKey.value = key;
};


</script>


<style lang="scss" scoped>
#header {
  position: fixed;
  width: 100%;
  height: 200px;
  overflow: hidden;
  background: #ffffff;
  align-items: center;
  padding: 0 30px;


  a {
    font-weight: 600;
    font-size: 40px;
    line-height: 48px;
    padding: 3px;
    color: #092d37;

  }

  .logo {
    display: flex;
    align-items: center;
    float: left;
    height: 64px;
    margin-top: 80px;
    margin-left: 100px;
  }
}

#components-layout {

  position: fixed;
  top: 0;
  left: 0;
  height: 10px;
  width: 100vw;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 1000;

  .menu {
    display: flex;
    list-style: none;
    margin: 0;
    padding: 0;
    z-index: 10000;

    li {
      margin-right: 20px;
    }


    a {
      font-weight: 600;
      font-size: 20px;
      color: black;
      padding: 0 30px; /* 추가: 메뉴 아이템 간격을 더 넓힘 */
    }

    .selected {
      border-bottom: 2px solid #1890ff;
    }
  }

  .col_left {
    display: flex;
    align-items: center;
    float: left;
    height: 64px;
    margin-top: 50px;
    margin-left: 100px;
  }
}

.nav-right {
  float: right;
  padding-right: 20px;
  padding-top: 20px;
  margin-left: auto;

  button {
    border-radius: 10px;
  }

  z-index: 100000;
}

.header-container {
  display: flex;
  align-items: center;
  float: left;
  height: 64px;
  margin-top: 50px;
  margin-left: 100px;
}

.menu-container {
  height: 70%;
  display: flex;
  align-items: center;
  float: right;
  margin-top: 50px;
  margin-left: 100px;
  margin-right: 10%;
}

.ant-btn {
  margin-left: 10px;
}

</style>