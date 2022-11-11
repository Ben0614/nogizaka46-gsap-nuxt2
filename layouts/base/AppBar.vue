<template>
  <div ref="header" class="header">
    <v-container>
      <v-img :style="{cursor:'pointer'}" width="200px" :src="require('@/assets/images//nogizaka46/Nogizaka46_logo_long.png')" contain @click="goToHome"></v-img>
    </v-container>
  </div>
</template>

<script>
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
export default {
  name: 'BaseAppBar',
  directives: {},
  components: {},
  data: () => ({}),

  computed: {},
  mounted() {
    // 如果需要設斷點 就用這個
    gsap.registerPlugin(ScrollTrigger)

    const showAnim = gsap
      .from(this.$refs.header, {
        yPercent: -100,
        paused: true,
        duration: 0.2,
      })
      .progress(1)

    ScrollTrigger.create({
      start: 'top top',
      end: 'bottom',
      onUpdate: (self) => {
        self.direction === -1 ? showAnim.play() : showAnim.reverse()
      },
    })
  },

  methods: {
    goToHome() {
      this.$router.push({ name: 'index' })
    },
  },
}
</script>
<style lang="scss" scoped>
$z-index-sub-topbar: 2;
$md: 959px;
$z-99: 99;

.header {
  position: fixed;
  box-shadow: none !important;
  width: 100%;
  height: 80px !important;
  border-bottom: 2px solid #1e3653;
  background-color: #fff;
  z-index: 100;
}

.z-999 {
  z-index: 999;
}

.v-list-item {
  min-height: 34px;
}
.top-bar {
  height: 40px;
  display: flex;
  align-items: center;
}
.sale-page-one {
  .sub-topbar {
    &.v-app-bar--is-scrolled {
      position: relative;
      .dropdown-ecommerce {
        display: none;
      }
    }
  }

  .navbar {
    &.v-app-bar--is-scrolled {
      top: 0;
      margin-bottom: 0px;
    }
  }
}
.sale-page-two {
  .sub-topbar {
    &.v-app-bar--is-scrolled {
      position: relative;
      .dropdown-ecommerce {
        display: none;
      }
    }
  }

  .navbar {
    &.v-app-bar--is-scrolled {
      top: 0;
      margin-bottom: 0px;
    }
  }
}

.sub-topbar {
  position: fixed;
  box-shadow: none !important;
  width: 100%;
  height: 80px !important;
  z-index: $z-99;

  @media (max-width: $md) {
  }
}

.navbar {
  height: 60px;
  width: 100%;
  z-index: 2;
  box-shadow: rgb(43 52 69 / 10%) 0px 16px 16px -16px !important;
  &.v-app-bar--is-scrolled {
    position: relative;
    top: 64px;
    margin-bottom: 64px;
    box-shadow: rgb(43 52 69 / 10%) 0px 16px 16px -16px !important;
    // box-shadow: none !important;
  }
  @media (max-width: 992px) {
    display: none;
  }
}
.search-bar {
  ::v-deep .v-input__slot {
    border: 1px solid rgb(218, 225, 231);
    background-color: #fff !important;
  }
  .search-bar-dropdown {
    height: 39px;
    position: absolute;
    top: 20px;
    transform: translateY(-50%);
    right: 2px;
    border-radius: 22px;
    border-top-left-radius: 0px;
    border-bottom-left-radius: 0px;
    border-left: 1px solid rgb(218, 225, 231) !important;
    box-shadow: none !important;
    @media (max-width: $md) {
      display: none;
    }
  }
  ::v-deep .v-text-field__details {
    display: none;
  }
}

// toggleNavbarButton
.navbar-toggle-dropdown {
  z-index: 98;
  display: none;
  &.open {
    display: block;
    top: 64px;
  }
}
.v-hidden {
  visibility: hidden;
}
.empty-cart-sidebar {
  height: 80vh;
}
</style>