<template>
  <div class="detailPage" :style="{paddingTop:isMobile ? '200px' :isNoteBook ? '150px' : '300px'}">
    <!-- transformOrigin:'top left' -->
    <span :style="{position:'fixed',top:'50%',left:'-10px',zIndex:'2',transform:'rotate(270deg)'}" class="company font-weight-bold">乃木坂合同會社</span>
    <span :style="{position:'fixed',top:'50%',right:'0',zIndex:'2',transform:'rotate(270deg)'}" class="company font-weight-bold">sony music</span>

    <div class="section1">
      <h1 :style="{position:'relative',lineHeight:'110%',zIndex:'2',width:'50%'}" class="rx90 text-center mx-auto" :class="isMobile ? 'text-h4' : isNoteBook ? 'text-h3' : 'text-h1'">乃木坂46は太陽みたいなグループ</h1>
      <div :style="{position:'fixed',top:'35%',left:'0',width:'100%'}" class="circleLine">
        <div :style="{position:'relative'}" class="semiCircle"></div>
        <div :style="{position:'relative'}" class="lineWrap d-flex flex-column align-center">
          <div v-for="(line) in 5" :key="line" class="line" :class="isNoteBook ? 'mb-5' : 'mb-7'"></div>
        </div>
      </div>
    </div>

    <v-container class="section2 py-10">
      <h1 :style="{position:'relative',zIndex:'2'}" class="rx90 text-center" :class="isMobile ? 'text-h5 mb-7' : isNoteBook ? 'text-h4 mb-10' : 'text-h3 mb-15'">31st「ここにはないもの」</h1>
      <div class="d-flex" :class="isMobile ? 'flex-column' : 'justify-space-around'">
        <!-- flex底下的元素好像可以直接用index 不用relative -->
        <div :style="{zIndex:'2'}" :class="isNoteBook ? 'd-flex' : ''">
          <div v-if="isMobile" class="d-flex flex-wrap">
            <h4 v-for="(pic,index) in pics" :key="index" class="rx90 picList" :class="'text-h6 ml-4'" @mouseenter="changePic(pic)">
              {{pic.number}}
            </h4>
          </div>
          <div v-if="!isMobile">
            <h4 v-for="(pic,index) in pics.slice(0,5)" :key="index" class="rx90 picList" :class="isNoteBook ? 'text-h5' : 'text-h4'" @mouseenter="changePic(pic)">
              {{pic.number}}
            </h4>
          </div>
          <div v-if="!isMobile" :class="isNoteBook ? 'ml-10' : ''">
            <h4 v-for="(pic,index) in pics.slice(5)" :key="index" class="rx90 picList" :class="isNoteBook ? 'text-h5' : 'text-h4'" @mouseenter="changePic(pic)">
              {{pic.number}}
            </h4>
          </div>
        </div>
        <div :style="{zIndex:'2'}" class="avatar">
          <v-img class="img" :src="activePic.src"></v-img>
        </div>
      </div>
    </v-container>

    <div class="circleBgWrap">
      <div v-for="circle in 5" :key="circle" class="circleBg"></div>
    </div>
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
    window.scrollTo(0, 0)
    console.log('Kokonihanaimonowindow.pageYOffset', window.pageYOffset)

    // 第一層區域高 要寫在最上面 (重要)
    // gsap.matchMedia 斷點設定 
    const heightMedia = this.$gsap.matchMedia('.detailPage')
    heightMedia
      .add('(min-width: 0px) and (max-width: 1319px)', () => {
        this.$gsap.set('.section1', {
          height: '750px',
        })
      })
      .add('(min-width: 1320px)', () => {
        this.$gsap.set('.section1', {
          height: '1350px',
        })
      })

    // 文字rotate
    const rxs = this.$gsap.utils.toArray('.rx90')
    rxs.forEach((item, index) => {
      this.$gsap.to(item, {
        scrollTrigger: {
          trigger: item,
          start: 'top bottom-=10%',
          end: 'top bottom-=10%',
          scrub: 1,
          // markers: true,
        },
        transform: 'rotateX(0)',
      })
    })
    // 線條
    const lines = this.$gsap.utils.toArray('.line')
    // 線條預設長度
    const widths = ['100%', '90%', '80%', '70%', '60%']
    // 線條
    lines.forEach((line, index) => {
      this.$gsap.set(line, {
        width: widths[index],
      })
      this.$gsap.to(line, {
        scrollTrigger: {
          trigger: '.lineWrap',
          scrub: 1,
          start: 'top center',
          end: 'top+=150 center-=100',
          // markers: true,
        },
        width: '100%',
        borderRadius: '0',
      })
    })
    // 半圓
    this.$gsap.to('.semiCircle', {
      scrollTrigger: {
        trigger: '.lineWrap',
        scrub: 1,
        start: 'top center',
        end: 'top+=150 center',
        // markers: true,
      },
      yPercent: 100,
    })
    // 整個半圓和線條區域 (position)
    this.$gsap.to('.circleLine', {
      // start end 用 bottom 為基準 兩個內容必須一樣
      // 因為原本fixed有top:35% 所以改成staic必須用translateY35%
      // 開始結束是bottom+=50% 所以translateY必須35%+50%
      scrollTrigger: {
        trigger: '.circleLine',
        start: 'bottom+=30% center',
        end: 'bottom+=30% center',
        scrub: true,
        // markers: true,
        // onUpdate: () => {
        //   const circleLine = document.querySelector('.circleLine')
        //   // 距離頂部的距離 + 自身的高 + 135
        //   // 135 是lineWrap的高度325 扣掉5條line+它們的mb總共190 後的高度
        //   // 不加135的話下方的區域會被擋到
        //   const section1Height =
        //     circleLine.offsetTop + circleLine.offsetHeight + 135
        //   console.log('section1Height', section1Height)
        //   this.$gsap.set('.section1', {
        //     height: () => section1Height,
        //   })
        // },
      },
      position: 'static',
      transform: 'translateY(65%)',
    })
    // 左右的fixed文字
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

    // 第二區域的背景圓球區域
    // 滑到第二區域才顯示
    this.$gsap.to('.circleBgWrap', {
      scrollTrigger: {
        trigger: '.section2',
        start: 'top center',
        end: 'top center',
        scrub: true,
        // markers: true,
      },
      display: 'block',
    })

    // 因為寬和高必須相同 所以在外面用random
    // const random = this.$gsap.utils.random(100, 300, 10, true)
    // const randoms = []
    // for (let i = 0; i < 5; i++) {
    //   randoms.push(random())
    // }

    // 圓球 個別調整
    const circileMedia = this.$gsap.matchMedia('.detailPage')
    circileMedia
      .add('(min-width: 0px) and (max-width: 959px)', () => {
        this.$gsap.set('.circleBg', {
          width: (i) => {
            if (i === 0) {
              return '100px'
            }
            if (i === 1) {
              return '125px'
            }
            if (i === 2) {
              return '500px'
            }
            if (i === 3) {
              return '0'
            }
            if (i === 4) {
              return '0'
            }
          },
          height: (i) => {
            if (i === 0) {
              return '100px'
            }
            if (i === 1) {
              return '125px'
            }
            if (i === 2) {
              return '500px'
            }
            if (i === 3) {
              return '0'
            }
            if (i === 4) {
              return '0'
            }
          },
          top: (i) => {
            if (i === 0) {
              return '10%'
            }
            if (i === 1) {
              return '60%'
            }
            if (i === 2) {
              return '15%'
            }
            if (i === 3) {
              return '0'
            }
            if (i === 4) {
              return '0'
            }
          },
          left: (i) => {
            if (i === 0) {
              return '5%'
            }
            if (i === 1) {
              return '0%'
            }
            if (i === 2) {
              return '30%'
            }
            if (i === 3) {
              return '0'
            }
            if (i === 4) {
              return '0'
            }
          },
          // width: (i) => randoms[i] + 'px',
          // height: (i) => randoms[i] + 'px',
          // top: 'random(0,90,10,true)%',
          // left: 'random(0,90,10,true)%',
          borderRadius: '50%',
        })
      })
      .add('(min-width: 960px)', () => {
        this.$gsap.set('.circleBg', {
          width: (i) => {
            if (i === 0) {
              return '100px'
            }
            if (i === 1) {
              return '125px'
            }
            if (i === 2) {
              return '500px'
            }
            if (i === 3) {
              return '100px'
            }
            if (i === 4) {
              return '150px'
            }
          },
          height: (i) => {
            if (i === 0) {
              return '100px'
            }
            if (i === 1) {
              return '125px'
            }
            if (i === 2) {
              return '500px'
            }
            if (i === 3) {
              return '100px'
            }
            if (i === 4) {
              return '150px'
            }
          },
          top: (i) => {
            if (i === 0) {
              return '10%'
            }
            if (i === 1) {
              return '40%'
            }
            if (i === 2) {
              return '15%'
            }
            if (i === 3) {
              return '15%'
            }
            if (i === 4) {
              return '70%'
            }
          },
          left: (i) => {
            if (i === 0) {
              return '5%'
            }
            if (i === 1) {
              return '15%'
            }
            if (i === 2) {
              return '30%'
            }
            if (i === 3) {
              return '85%'
            }
            if (i === 4) {
              return '95%'
            }
          },
          borderRadius: '50%',
        })
      })

    // 讓圓球外觀動畫改變
    this.$gsap.to('.circleBg', {
      keyframes: [
        {
          borderRadius: '63% 37% 54% 46% / 55% 48% 52% 45%',
          duration: 3,
        },
        {
          borderRadius: '40% 60% 45% 55% / 49% 60% 40% 51%',
          duration: 3,
        },
        {
          borderRadius: '50% 50% 34% 66% / 56% 68% 32% 44%',
          duration: 3,
        },
        {
          borderRadius: '46% 54% 50% 50% / 35% 61% 39% 65%',
          duration: 3,
        },
      ],
      repeat: -1,
      yoyo: true,
    })
    // 圖片的list
    // 觸碰到就改變文字顏色並加上底線
    // 其他兄弟選項就恢復原狀
    const picList = this.$gsap.utils.toArray('.picList')
    picList.forEach((item, index) => {
      // 預設選中第一個
      if (index === 0) {
        this.$gsap.set(item, {
          color: '#000',
          borderBottom: '1px solid #000',
        })
      }
      item.addEventListener('mouseenter', () => {
        // item和兄弟item的style必須都要寫 (color、borderBottom、duration)
        // 如果item有duration 兄弟item沒有 就會有bug
        this.$gsap.to(item, {
          color: '#000',
          borderBottom: '1px solid #000',
          duration: 0.3,
        })
        // 其他兄弟item
        picList.forEach((children, index) => {
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
    // 大圖片
    this.$gsap.set('.avatar', {
      borderRadius: '61% 39% 57% 43% / 46% 67% 33% 54%',
    })
    // 大圖片外形動畫
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
.rx90 {
  transform: rotateX(90deg);
}
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

  @media screen and (max-width: '1319px') {
    width: 350px;
    height: 175px;
    border-radius: 350px 350px 0 0;
  }
}
.lineWrap {
  min-height: 325px;
  background-color: rgba(246, 249, 252);
  @media screen and (max-width: '1319px') {
    min-height: 175px;
  }

  .line {
    height: 10px;
    border-radius: 0 0 10px 10px;
    background: linear-gradient(
      to right,
      lightblue,
      rgb(173, 173, 255),
      lightpink
    );
  }
}

.picList {
  cursor: pointer;
  font-weight: bold;
  margin: 0 0 20px 0;
  color: rgba(128, 128, 128, 0.5);
}

.avatar {
  width: 600px;
  height: 600px;
  max-width: 100%;
  object-fit: 'cover';
  overflow: hidden;

  @media screen and (max-width: '1319px') {
    width: 450px;
    height: 450px;
  }

  .img {
    width: 100%;
    height: 100%;
  }
}
.circleBgWrap {
  display: none;
  position: fixed;
  z-index: 0;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  .circleBg {
    position: absolute;
    opacity: 0.6;
    background: linear-gradient(to right, #d964e6, #9198e5);
  }
}
</style>


