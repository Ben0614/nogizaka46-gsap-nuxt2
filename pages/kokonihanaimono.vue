<template>
  <div :style="{padding:'300px 0 0 0'}">
    <!-- transformOrigin:'top left' -->
    <span :style="{position:'fixed',top:'50%',left:'-10px',zIndex:'2',transform:'rotate(270deg)'}" class="company font-weight-bold">乃木坂合同會社</span>
    <span :style="{position:'fixed',top:'50%',right:'0',zIndex:'2',transform:'rotate(270deg)'}" class="company font-weight-bold">sony music</span>

    <div class="section1">
      <h1 :style="{position:'relative',lineHeight:'110%',zIndex:'2',width:'50%'}" class="text-h1 text-center mx-auto">乃木坂46は太陽みたいなグループ</h1>
      <div :style="{position:'fixed',top:'35%',left:'0',width:'100%'}" class="circleWave">
        <div :style="{position:'relative'}" class="semiCircle"></div>
        <div :style="{position:'relative'}" class="waveWrap d-flex flex-column align-center">
          <div v-for="(wave) in 5" :key="wave" class="wave mb-7"></div>
        </div>
      </div>
    </div>

    <v-container class="section2 py-10">
      <h1 class="text-h3 text-center mb-15">31st「ここにはないもの」</h1>
      <div class="d-flex justify-space-around">
        <div>
          <h4 v-for="(pic,index) in pics" :key="index" class="picList text-h4" @mouseenter="changePic(pic)">
            {{pic.number}}
          </h4>
        </div>
        <div class="avatar">
          <v-img class="img" :src="activePic.src"></v-img>
        </div>
      </div>
    </v-container>
  </div>
</template>

<script>
export default {
  name: 'Kokonihanaimono',
  components: {},
  data() {
    return {
      pics: [
        {
          number: 'One',
          src: require('@/assets/images/nogizaka46/31st/1.jpg'),
        },
        {
          number: 'Two',
          src: require('@/assets/images/nogizaka46/31st/2.jpg'),
        },
        {
          number: 'Three',
          src: require('@/assets/images/nogizaka46/31st/3.jpg'),
        },
        {
          number: 'Four',
          src: require('@/assets/images/nogizaka46/31st/4.jpg'),
        },
        {
          number: 'Five',
          src: require('@/assets/images/nogizaka46/31st/5.jpg'),
        },
        {
          number: 'Six',
          src: require('@/assets/images/nogizaka46/31st/6.jpg'),
        },
        {
          number: 'Seven',
          src: require('@/assets/images/nogizaka46/31st/7.jpg'),
        },
        {
          number: 'Eight',
          src: require('@/assets/images/nogizaka46/31st/8.jpg'),
        },
        {
          number: 'Night',
          src: require('@/assets/images/nogizaka46/31st/9.jpg'),
        },
        {
          number: 'Ten',
          src: require('@/assets/images/nogizaka46/31st/10.jpg'),
        },
      ],
      activePic: {
        number: 'One',
        src: require('@/assets/images/nogizaka46/31st/1.jpg'),
      },
    }
  },

  computed: {
    isMobile() {
      return ['xs', 'sm'].includes(this.$vuetify.breakpoint.name)
    },
    isNoteBook() {
      return ['md'].includes(this.$vuetify.breakpoint.name)
    },
  },

  mounted() {
    console.log('window.pageYOffset', window.pageYOffset)

    const waves = this.$gsap.utils.toArray('.wave')
    const widths = ['100%', '90%', '80%', '70%', '60%']
    this.$gsap.set('.section1', {
      height: '1461px',
    })

    waves.forEach((wave, index) => {
      this.$gsap.set(wave, {
        width: widths[index],
      })
      this.$gsap.to(wave, {
        scrollTrigger: {
          trigger: '.waveWrap',
          scrub: 1,
          start: 'top center',
          end: 'top+=150 center-=100',
          // markers: true,
        },
        width: '100%',
        borderRadius: '0',
      })
    })
    this.$gsap.to('.semiCircle', {
      scrollTrigger: {
        trigger: '.waveWrap',
        scrub: 1,
        start: 'top center',
        end: 'top+=150 center',
        // markers: true,
      },
      yPercent: 100,
    })

    this.$gsap.to('.circleWave', {
      // start end 用 bottom 為基準 兩個內容必須一樣
      // 因為原本fixed有top:35% 所以改成staic必須用translateY35%
      // 開始結束是bottom+=50% 所以translateY必須35%+50%
      scrollTrigger: {
        trigger: '.circleWave',
        start: 'bottom+=30% center',
        end: 'bottom+=30% center',
        scrub: true,
        markers: true,
        // onUpdate: () => {
        //   const circleWave = document.querySelector('.circleWave')
        //   // 距離頂部的距離 + 自身的高 + 135
        //   // 135 是waveWrap的高度325 扣掉5條wave+它們的mb總共190 後的高度
        //   // 不加135的話下方的區域會被擋到
        //   const section1Height =
        //     circleWave.offsetTop + circleWave.offsetHeight + 135
        //   console.log('section1Height', section1Height)
        //   this.$gsap.set('.section1', {
        //     height: () => section1Height,
        //   })
        // },
      },
      position: 'static',
      transform: 'translateY(65%)',
    })

    const handleCompany = this.$gsap
      .from('.company', {
        xPercent: (i) => (i === 0 ? -100 : 100),
        paused: true,
      })
      .progress(1)

    this.$scrollTrigger.create({
      onUpdate: (self) => {
        if (window.pageYOffset <= 0) {
          handleCompany.play()
        }
        if (window.pageYOffset > 0) {
          handleCompany.reverse()
        }
      },
    })

    const picList = this.$gsap.utils.toArray('.picList')
    picList.forEach((item, index) => {
      if (index === 0) {
        this.$gsap.set(item, {
          color: '#000',
          borderBottom: '1px solid #000',
        })
      }
      const p = item.parentNode.children
      item.addEventListener('mouseenter', () => {
        // item和兄弟item的style必須都要寫 (color、borderBottom、duration)
        // 如果item有duration 兄弟item沒有 就會有bug
        this.$gsap.to(item, {
          color: '#000',
          borderBottom: '1px solid #000',
          duration: 0.3,
        })

        p.forEach((children, index) => {
          if (children !== item) {
            this.$gsap.to(children, {
              color: 'rgba(128,128,128,0.5)',
              borderBottom: 'none',
              duration: 0.3,
            })
          }
        })
      })
    })

    this.$gsap.set('.avatar', {
      borderRadius: '61% 39% 57% 43% / 46% 67% 33% 54%',
    })
    this.$gsap.to('.avatar', {
      keyframes: [
        {
          borderRadius: '58% 42% 59% 41% / 52% 46% 54% 48%',
          duration: 3,
        },
        {
          borderRadius: '46% 54% 40% 60% / 52% 33% 67% 48%',
          duration: 3,
        },
        {
          borderRadius: '65% 35% 71% 29% / 31% 60% 40% 69%',
          duration: 3,
        },
        {
          borderRadius: '60% 40% 43% 57% / 45% 51% 49% 55%',
          duration: 3,
        },
      ],
      repeat: -1,
      yoyo: true,
    })

    // const t = this.$gsap.timeline({
    //   repeat: -1,
    //   yoyo: true,
    //   defaults: {
    //     duration: 3,
    //   },
    // })
    // t.to('.avatar', {
    //   borderRadius: '58% 42% 59% 41% / 52% 46% 54% 48%',
    // })
    //   .to('.avatar', { borderRadius: '46% 54% 40% 60% / 52% 33% 67% 48%' })
    //   .to('.avatar', { borderRadius: '65% 35% 71% 29% / 31% 60% 40% 69%' })
    //   .to('.avatar', { borderRadius: '60% 40% 43% 57% / 45% 51% 49% 55%' })
  },
  methods: {
    changePic(pic) {
      this.activePic = Object.assign({}, pic)
    },
  },
}
</script>
<style lang="scss" scoped>
.semiCircle {
  width: 650px;
  height: 325px;
  margin: 0 auto;
  border-radius: 650px 650px 0 0;
  background: linear-gradient(
    to right,
    lightblue,
    rgb(173, 173, 255),
    lightpink
  );
}
.waveWrap {
  min-height: 325px;
  background-color: rgba(246, 249, 252);
}
.wave {
  height: 10px;
  border-radius: 0 0 10px 10px;
  background: linear-gradient(
    to right,
    lightblue,
    rgb(173, 173, 255),
    lightpink
  );
}
.picList {
  cursor: pointer;
  font-weight: bold;
  margin: 0 0 20px 0;
  color: rgba(128, 128, 128, 0.5);
  /* &:hover {
    color: #000;
    border-bottom: 1px solid #000;
    transition: 0.3s;
  } */
}

.avatar {
  width: 40%;
  overflow: hidden;

  .img {
    width: 100%;
    height: 100%;
  }
}
</style>


