<template>
  <v-btn :color="btnColor" :style="cssProps" class="btnWrap" rounded outlined large>
    <div class="btn-circle"></div>
    <span class="btn-text">{{content}}</span>
  </v-btn>
</template>

<script>
export default {
  name: 'BtnNormal',

  props: {
    content: {
      type: String,
      default: '',
    },
    btnColor: {
      type: String,
      default: '',
    },
    textColor: {
      type: String,
      default: 'black',
    },
    textHoverColor: {
      type: String,
      default: 'white',
    },
    circleColor: {
      type: String,
      default: 'skyblue',
    },
    time: {
      type: String,
      default: '0.3',
    },
  },
  computed: {
    cssProps() {
      return {
        '--text-color': this.textColor,
        '--text-hover-color': this.textHoverColor,
        '--time': `${this.time}s`,
        '--circle-color': this.circleColor,
      }
    },
  },
}
</script>

<style lang="scss" scoped>
.btnWrap {
  position: relative;
  overflow: hidden;

  .btn-circle {
    position: absolute;
    left: 0px;
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--circle-color);
    z-index: 0;
    transition: var(--time);
  }
  .btn-text {
    position: relative;
    z-index: 1;
    margin-left: 12px;
    color: var(--text-color);
  }

  &:hover .btn-circle {
    transition: var(--time);
    scale: 50;
  }
  &:hover .btn-text {
    color: var(--text-hover-color);
  }
}
</style>
