<template>
  <v-main class="main-content bg-body" :style="{marginTop:'80px'}">
    <v-fade-transition mode="out-in">
      <Nuxt />
    </v-fade-transition>
  </v-main>
</template>

<script>
  export default {
    name: 'BaseView',
  }
</script>
<style lang="scss" scoped>
  .main-content {
    padding: 0px 0px 0px !important;
  }
</style>
