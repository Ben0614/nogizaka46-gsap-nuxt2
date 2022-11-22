<template>
  <v-footer dark>
    <v-container class="d-flex">
      <h3 :style="{cursor:'pointer'}" class="text-h5 white--text" @click="goToPage('index')">Home</h3>
      <h3 :style="{cursor:'pointer'}" class="text-h5 ml-10 white--text" @click="goToPage('detail')">Join Us</h3>
      <h3 :style="{cursor:'pointer'}" class="text-h5 ml-10 white--text" @click="goToPage('kokonihanaimono')">31st</h3>
    </v-container>
  </v-footer>
</template>
<script>
export default {
  name: 'Footer',
  data: () => ({}),
  methods: {
    goToPage(paegName) {
      this.$router.push({ name: paegName })
    },
  },
}
</script>
<style lang="scss">
.v-footer {
  padding-top: 100px !important;
  padding-bottom: 100px !important;
  background: rgb(128, 0, 128, 0.7) !important;
}
</style>