<template>
  <v-app>
    <base-app-bar />

    <base-view />

    <footer-view />
    <!-- 滾動進度條 -->
    <!-- <div class="progress"></div> -->
    <div class="progress" :style="{height:progressHeight+'%'}"></div>
  </v-app>
</template>

<script>
export default {
  name: 'BaseLayout',
  components: {
    BaseAppBar: () => import('./base/AppBar'),
    BaseView: () => import('./base/View'),
    FooterView: () => import('./base/Footer'),
  },
  data() {
    return {
      progressHeight: 0,
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleProgress)
  },
  methods: {
    handleProgress() {
      // 頁面總高度 document.body.scrollHeight
      // 視窗高度 window.innerHeight
      // 滾動距離 window.pageYOffset
      // 步驟一 頁面總高度 - 視窗高度 (因為螢幕畫面的頂部無法到頁面最底部)
      // 步驟二 滾動距離 / 減完的總高度 (取百分比)
      // Math.round((num + Number.EPSILON) * 100) / 100; 可以四捨五入到小數點2位
      // 步驟三 結果 * 100 (因為取到的會是0.xx的格式 要變成%)
      const height =
        Math.round(
          (window.pageYOffset /
            (document.body.scrollHeight - window.innerHeight) +
            Number.EPSILON) *
            100
        ) / 100
      this.progressHeight = height * 100
    },
  },
}
</script>

<style lang="scss" scoped>
.progress {
  position: fixed;
  top: 0;
  left: 0;
  width: 5px;
  height: 0%;
  background-color: #812990;
  z-index: 100;
}
</style>