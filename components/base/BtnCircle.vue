<template>
  <v-btn width="50" height="50" icon :style="cssProps" class="btnCircle" @click="handleClick(fnName)">
    <v-icon size="30">{{iconName}}</v-icon>
  </v-btn>
</template>

<script>
export default {
  name: 'BtnCircle',

  props: {
    iconName: {
      required: true,
      type: String,
    },
    btnColor: {
      type: String,
      default: 'white',
    },
    btnHoverColor: {
      type: String,
      default: 'gray',
    },
    iconColor: {
      type: String,
      default: 'black',
    },
    iconHoverColor: {
      type: String,
      default: 'white',
    },
    time: {
      type: String,
      default: '0',
    },
    // 點擊後要調用的function name
    fnName:{
      type: String,
      default: '',
    }
  },
  computed: {
    cssProps() {
      return {
        '--btn-color': this.btnColor,
        '--btn-hover-color': this.btnHoverColor,
        '--icon-color': this.iconColor,
        '--icon-hover-color': this.iconHoverColor,
        '--time': `${this.time}s`,
      }
    },
  },
  methods:{
    handleClick(fnName){
      this.$emit(fnName)
    }
  }
}
</script>

<style lang="scss" scoped>
.btnCircle {
  margin: 0 0 8px;
  background-color: var(--btn-color);
  transition: var(--time);
  .v-btn__content {
    .v-icon {
      color: var(--icon-color);
      transition: var(--time);
    }
  }

  &:hover {
    background-color: var(--btn-hover-color);
    transition: var(--time);
    .v-icon {
      color: var(--icon-hover-color);
      transition: var(--time);
    }
  }
}
</style>
