<template>
  <div>
    <div class="playCircleWrap" @click="openVideo">
      <p class="text-center white--text mb-1">PLAY FULL MOVIE</p>
      <div class="circleWhite">
        <div class="circleRed">
          <v-icon color="#fff">mdi-play</v-icon>
        </div>
      </div>
    </div>
    <v-dialog v-model="_dialogVisible" fullscreen persistent>
      <v-card width="100%" height="100%" :style="{background:'rgba(0,0,0,0.7)'}" class="d-flex justify-center align-center">
        <div class="d-flex" :style="{width:isMobile ? '100%' : '50%',height:'50%'}">
          <iframe width="100%" height="100%" :src="youtubePath" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
          <v-btn icon class="ml-15" :class="isMobile ? 'closeBtn' : ''" @click="dialogClose">
            <v-icon size="60px" color="#fff">mdi-close</v-icon>
            <span class="white--text">close</span>
          </v-btn>
        </div>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  name: 'PlayCircle',
  props: {
    dialogVisible: {
      type: Boolean,
      required: true,
    },
    youtubePath: {
      type: String,
      default: '',
      required: true,
    },
  },
  data() {
    return {}
  },
  computed: {
    _dialogVisible: {
      get() {
        return this.dialogVisible
      },
      set(val) {
        this.dialogClose()
      },
    },
    isMobile() {
      return ['xs', 'sm'].includes(this.$vuetify.breakpoint.name)
    },
  },
 
  methods: {
    openVideo() {
      this.$emit('openVideo', true)
    },
    // 關閉彈窗
    dialogClose() {
      this.$emit('dialogClose', false)
    },
  },
}
</script>

<style lang="scss">
.playCircleWrap {
  /* position: absolute;
  z-index: 2;
  bottom: -80px;
  right: 100px; */
  background: transparent;
  cursor: pointer;

  &:hover .circleRed {
    width: 160px;
    height: 160px;
    transition: 0.3s;
  }

  .circleWhite,
  .circleRed {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 160px;
    height: 160px;
    background: #fff;
    border-radius: 50%;
  }

  .circleRed {
    width: 120px;
    height: 120px;
    background: red;
    transition: 0.3s;
  }
}

.closeBtn{
    position: absolute;
    top:30px;
    right:30px
  }
</style>