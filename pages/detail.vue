<template>
  <div class="wrap white--text">
    <!-- section1 -->
    <!-- ,clipPath: 'inset(0)' *現在沒在用 -->
    <div :style="{position:'relative',width:'100%',height:'100%',zIndex:0}" class="section1">
      <!-- 背景影片 -->
      <!-- transform:'rotateY(180deg)' *現在沒在用 -->
      <!-- objectFit:'cover' 手機版一定要加這個 影片才會100vh高 -->
      <video ref="bannerVideo" :style="{width:'100%',height:isMobile ? '100vh' : '',objectFit:'cover'}" src="@/assets/video/2ndAlbum.mp4" autoplay muted loop></video>
      <!-- 黑色遮罩 -->
      <div class="video-bg"></div>
      <!-- 文字內容 -->
      <v-container :style="{position:'absolute',bottom:'85px',left:'0',zIndex:2}" class="d-flex justify-space-between align-end">
        <div class="videoText">
          <h1 class="slide-up section1Title mb-10" :class="isMobile ? 'text-h5' : isNoteBook ? 'text-h3' : 'text-h1'">乃木坂46 新メンバー募集開始</h1>
          <p class="fade section1Content" :class="isMobile ? '' : isNoteBook ? 'text-body-1' : 'text-h5'">
            誰にも言えていない、夢がある？
            <br>
            あの人のどこに、憧れている？
            <br>
            本気で、泣いて笑って、青春してる？
            <br>
            背中を押してくれる何かを、待ってる？
            <br>
            たった一度の夏、
            <br>
            たった一度の、きみへ。
            <br>
            乃木坂46 新メンバー募集開始
            <br>
            この世界の、未完成は美しい。
          </p>
        </div>
        <!-- gsap控制 -->
        <BtnCircle :icon-name="'mdi-chevron-down'" :btn-color="'white'" :btn-hover-color="'gray'" :icon-color="'black'" :icon-hover-color="'white'" :time="'0.3'" class="bannerVideoBtn"></BtnCircle>

        <!-- 純js控制 -->
        <!-- fn-name 點擊後要調用的function name -->
        <!-- <BtnCircle :icon-name="'mdi-chevron-down'" :btn-color="'white'" :btn-hover-color="'gray'" :icon-color="'black'" :icon-hover-color="'white'" :time="'0.3'" :fn-name="'goToSection2'" @goToSection2="goToSection2"></BtnCircle> -->

      </v-container>
    </div>

    <!-- section2 -->
    <div class="section2 bg py-10">
      <!-- card -->
      <v-container class="mb-15">
        <h1 class="mb-10" :class="isMobile ? 'text-h5' : 'text-h2'">私たちの番組</h1>
        <v-row>
          <v-col v-for="(card,index) in cards" :key="index" cols="12" md="4">
            <div class="processCard rounded-lg py-8 px-5">
              <!-- 背景影片 -->
              <!-- scale 和 rotate不能同時寫在同一個tag裡 需要的話要外面再包一層 -->
              <video src="@/assets/video/2ndAlbum.mp4" autoplay muted loop></video>
              <!-- 文字區域 -->
              <div :style="{position:'relative',height:'100%'}" class="d-flex flex-column justify-space-between">
                <div>
                  <p>{{`${index + 1}. ${card.type}`}}</p>
                  <h3 class="mb-8">{{card.title}}</h3>
                  <p>{{card.content}}</p>
                </div>
                <div class="d-flex justify-space-between align-end">
                  <div :style="{width:'120px'}">
                    <v-img :src="require('@/assets/images/nogizaka46/Nogizaka46_logo.png')"></v-img>
                  </div>
                  <BtnCircle :icon-name="'mdi-plus'" :btn-color="'gray'" :btn-hover-color="'white'" :icon-color="'white'" :icon-hover-color="'black'"></BtnCircle>
                  <!-- <v-btn width="50" height="50" icon class="plusBtn">
                    <v-icon size="30">mdi-plus</v-icon>
                  </v-btn> -->
                </div>
              </div>
            </div>
          </v-col>
        </v-row>
      </v-container>
      <!-- 跑馬燈 -->
      <div class="marquee my-15">
        <div class="boxes">
          <div class="box">Nogizaka46</div>
          <div class="box">乃木坂46</div>
          <div class="box">Nogizaka46</div>
          <div class="box">乃木坂46</div>
          <div class="box">Nogizaka46</div>
          <div class="box">乃木坂46</div>
        </div>
      </div>

      <v-container>
        <v-row justify="center">
          <v-expansion-panels v-model="activeExpand" accordion tile dark>
            <v-expansion-panel v-for="(item,index) in expansionData" :key="index" :style="{borderTop:index === 0 ? '1px solid #fff' : '',borderBottom:'1px solid #fff'}">
              <v-expansion-panel-header color="#0e0e0e" class="white--text" hide-actions>
                <div class="d-flex justify-space-between align-center">
                  <h4>{{item.title}}</h4>
                  <div class="expandArea">
                    <v-btn icon class="expandBtn" x-large>
                      <v-icon :style="{transform: index === activeExpand ? 'rotate(180deg)' : ''}">mdi-chevron-down</v-icon>
                    </v-btn>
                    <div class="btnOverlay"></div>
                  </div>
                </div>
              </v-expansion-panel-header>
              <v-expansion-panel-content color="#0e0e0e" class="white--text">
                {{item.content}}
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels>
        </v-row>
      </v-container>
    </div>

    <!-- 卡片側邊欄 -->
    <v-navigation-drawer v-model="drawer" fixed app temporary right :width="isMobile ? '100%' : '40%'" :style="{zIndex:100}" class="" :class="isMobile ? 'py-15 px-3' : 'py-5 px-15'">
      <v-btn :style="{position:'absolute',top:'20px',right:'20px'}" icon class="black" @click="drawer = false">
        <v-icon color="white">mdi-close</v-icon>
      </v-btn>
      <v-tabs v-model="tab" :show-arrows="isMobile ? true : false" background-color="transparent" color="black" grow class="mb-5">
        <v-tab v-for="(item,index) in drawerDatas" :key="index" class="mx-3">
          {{ item.tab }}
        </v-tab>
      </v-tabs>

      <v-tabs-items v-model="tab">
        <v-tab-item v-for="(item,index) in drawerDatas" :key="index">
          <v-card flat>
            <v-card-text>
              <h3 class="text-h5 font-weight-bold mb-3">{{item.title}}</h3>
              <p>{{ item.content }}</p>
              <a :href="item.url" target="_blank" class="purple--text">ここをクリック</a>
            </v-card-text>
          </v-card>
        </v-tab-item>
      </v-tabs-items>
    </v-navigation-drawer>
  </div>
</template>

<script>
// import AOS from 'aos'
// import { WOW } from 'wowjs'
import BtnCircle from '@/components/base/BtnCircle'
export default {
  name: 'Detail',
  components: {
    BtnCircle,
  },
  data() {
    return {
      // 背景影片
      // videoUrl:
      //   'https://player.vimeo.com/progressive_redirect/playback/703186983/rendition/1080p?loc=external&signature=0295f802f1d2573f68e79c70168d733450a751c94901c6e8f9934575131f90aa',
      // videoUrl: '@/assets/video/2ndAlbum.mp4',
      // 卡片資料
      expansionData: [
        { title: '結成時間', content: '2021/8/21' },
        { title: '專輯數量', content: '31' },
        { title: '紅白次數', content: '7' },
        { title: '成員總期數', content: '5' },
      ],
      activeExpand: null,
      cards: [
        {
          type: '冠名綜藝番組',
          title: '乃木坂工事中',
          content:
            '2015年（平成27年）4月20日からテレビ愛知の企画・制作により、テレビ東京系列などで放送されている乃木坂46の冠バラエティ番組である',
        },
        {
          type: '冠名歌唱番組',
          title: '新乃木之星誕生',
          content:
            '2021年5月11日（10日深夜）から2022年3月8日（7日深夜）まで日本テレビで放送されていた乃木坂46のバラエティ番組である',
        },
        {
          type: 'Youtubeチャネル',
          title: '乃木坂配信中',
          content:
            '乃木坂46 ２つ目の公式YouTubeチャンネルです。このチャンネルでは、主に乃木坂工事中(毎週日曜深夜0:00〜 テレビ愛知発全国ネットにて放送中)の無料配信、また、ここでしか見られないオリジナルコンテンツを不定期で配信予定です！',
        },
      ],
      // 卡片側邊欄
      drawer: false,
      tab: 0,
      // 側邊欄資料
      drawerDatas: [
        {
          tab: '冠名綜藝番組',
          title: '乃木坂工事中',
          content:
            '乃木坂46にとって初の地上波レギュラー冠番組だった『乃木坂って、どこ?』（2011年10月3日 - 2015年4月13日）をリニューアルした後継番組[2]。『乃木坂って、どこ?』に引き続き、MCはバナナマンが担当[2]。番組名の『乃木坂工事中』は乃木坂46の総合プロデューサー・秋元康が考案した[3]。2016年12月30日、『乃木坂って、どこ?』時代から通じて初の特番となる1時間SPを放送[4]。本番組のネット局であるテレビ東京に限り当番組の後に放送されている『欅って、書けない?』（関東ローカル）に出演する[5]、同じ坂道シリーズの欅坂46との合同忘年会企画を行った[6]。以後、2017年12月25日、2018年1月8日、2019年1月7日に拡大1時間SPを放送した[注 1][7][8]。2021年5月17日（16日深夜）放送回より、同月6日に新たに開設された乃木坂46のYouTubeチャンネル「乃木坂配信中」にて放送後に毎週無料配信されている[9][10]。地上波の番組をYouTubeにて公式無料配信するのは異例のことである[9][11]。番組の休止は年末年始を除いてほとんどないが、海外の時差の大きい世界卓球選手権などのスポーツ中継[注 2]が放送されるときは時間繰り下げや休止[注 3]となる場合がある[12]。',
          url: 'https://tv-aichi.co.jp/nogi-kou/',
        },
        {
          tab: '冠名歌唱番組',
          title: '新乃木之星誕生',
          content:
            '乃木坂46の5期生が過去に4期生が挑戦した『乃木坂スター誕生!』で「昭和歌謡」「平成の名曲」のヒットソングに挑戦する番組[2]。司会はお笑いコンビ・オズワルドが務め、当番組で初コラボとなる。 5期生にとっては当番組が初めての単独レギュラー番組となる。放送終了後、未公開映像を併せて「新・乃木坂スター誕生! 5期生の挑戦」のタイトルでHuluで配信',
          url: 'https://www.ntv.co.jp/newnogistar/',
        },
        {
          tab: 'Youtubeチャネル',
          title: '乃木坂配信中',
          content:
            '乃木坂46 ２つ目の公式YouTubeチャンネルです。このチャンネルでは、主に乃木坂工事中(毎週日曜深夜0:00〜 テレビ愛知発全国ネットにて放送中)の無料配信、また、ここでしか見られないオリジナルコンテンツを不定期で配信予定です！※既存の乃木坂46 official YouTubeチャンネルでは、今まで同様に音楽コンテンツを中心に配信していきます。チャンネル登録よろしくお願いします♪',
          url: 'https://www.youtube.com/c/nogizakahaishinchu',
        },
      ],
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
    console.log('Detail window.pageYOffset', window.pageYOffset)
    // aos
    // AOS.init()
    // wow
    // new WOW({ live: false }).init()

    // slide-up fade
    const t = this.$gsap.timeline({
      scrollTrigger: {
        trigger: '.videoText',
        start: 'top bottom',
        // markers: true,
      },
      defaults: {
        opacity: 0,
      },
    })
    t.from('.slide-up', {
      y: 800,
    }).from('.fade', {})

    // 視差
    // section1 影片區 100vh
    this.$scrollTrigger.create({
      trigger: '.section1',
      start: 'top top',
      pin: true,
      pinSpacing: false,
      // markers: true,
    })
    // section2 內容區 高度由內容撐開 所以必須給end: 'top top' 否則只能看到局部的內容
    this.$scrollTrigger.create({
      trigger: '.section2',
      start: 'top top',
      end: 'top top',
      pin: true,
      pinSpacing: false,
      // markers: true,
    })
    // 暫時不用
    // // 如果往下滑動 就讓大video top變0
    // const videoUp = gsap.to('.wrap', {
    //   marginTop: 0,
    //   paused: true,
    //   duration: 0.2,
    // })

    // this.$scrollTrigger.create({
    //   start: 'top top',
    //   onUpdate: (self) => {
    //     // 往下滑動是1 往上滑動是-1
    //     self.direction === 1 ? videoUp.play() : videoUp.reverse()
    //   },
    // })

    // 到第二區域btn
    const section2Top = document.querySelector('.section1').offsetHeight + 80 // 80 header高
    const bannerVideoBtn = document.querySelector('.bannerVideoBtn')
    bannerVideoBtn.addEventListener('click', () => {
      this.$gsap.to(window, {
        duration: 0.5,
        scrollTo: {
          y: section2Top,
        },
      })
    })

    // 卡片hover和click
    const cards = this.$gsap.utils.toArray('.processCard')
    const cardBtns = this.$gsap.utils.toArray('.processCard .btnCircle')
    const cardBtnIcons = this.$gsap.utils.toArray(
      '.processCard .btnCircle .v-icon'
    )
    cards.forEach((card, index) => {
      // 點擊就打開側邊欄 並指定tab
      card.addEventListener('click', () => {
        this.tab = index
        this.drawer = true
      })
      card.addEventListener('mouseenter', () => {
        this.$gsap.to(cardBtns[index], {
          backgroundColor: '#fff',
        })
        this.$gsap.to(cardBtnIcons[index], {
          color: '#000',
        })
      })
      card.addEventListener('mouseleave', () => {
        this.$gsap.to(cardBtns[index], {
          backgroundColor: 'gray',
        })
        this.$gsap.to(cardBtnIcons[index], {
          color: '#fff',
        })
      })
    })

    // 跑馬燈
    // gsap.utils.toArray 和 document.querySelectorAll 可以通用
    // getBoundingClientRect()  回傳元素的大小，以及其相對於可視範圍 (viewport) 的位置
    const box = document.querySelector('.box')
    const boxWidth = box.getBoundingClientRect().width
    const boxQuantity = document.querySelectorAll('.box').length
    const totalWidth = boxWidth * boxQuantity
    const marqueeWrapper = document.querySelectorAll('.box')
    const dirFromRight = '-=' + totalWidth

    console.log('boxWidth', boxWidth, 'boxQuantity', boxQuantity)

    const mod = this.$gsap.utils.wrap(0, totalWidth)
    // function裡 無法直接用this
    const gsap = this.$gsap
    function marquee(which, time, direction) {
      gsap.set(which, {
        x(i) {
          return i * boxWidth
        },
      })

      const action = gsap.timeline({ overwrite: true }).to(which, {
        x: direction,
        modifiers: {
          x: (x) => mod(parseFloat(x)) + 'px',
        },
        duration: time,
        ease: 'none',
        repeat: -1,
      })
      return action
    }

    const right = this.$gsap
      .timeline({ paused: true })
      .add(marquee(marqueeWrapper, 10, dirFromRight))

    right.play()
  },
  methods: {
    // 到第2區域
    // goToSection2() {
    //   // 80 header高
    //   const top = document.querySelector('.section2').offsetTop + 80
    //   const scrollToTop = window.setInterval(function () {
    //     const pos = window.pageYOffset
    //     if (pos < top) {
    //       window.scrollTo(0, pos + 20) // 每一次滾動多遠
    //     } else {
    //       window.clearInterval(scrollToTop)
    //     }
    //   }, 10)
    // },
  },
}
</script>

<style lang="scss">
.bg {
  background-color: #0e0e0e;
}

.video-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  z-index: 0;
}

.processCard {
  position: relative;
  height: 600px;
  border: 1px solid gray;
  cursor: pointer;
  overflow: hidden;
  @media screen and (max-width: '960px') {
    height: 500px;
  }
  video {
    position: absolute;
    height: 100%;
    top: 0;
    left: 0;
    z-index: 0;
    opacity: 0;
    transition: 0.3s;
  }
  &:hover video {
    opacity: 1;
    transition: 0.3s;
  }
}

/* width 150% 會造成爆版 這頁最外層用overflow hidden */
.marquee {
  width: 150%; // width必須大一點 否則有些字會瞬間消失
  height: 50px;
  /* overflow: hidden; */

  .boxes {
    position: relative;
    left: -16.6666%; // 會消除掉的位置
    height: 50px;
    @media screen and (max-width: 960px) {
      left: -33.3333%;
    }
  }
  .box {
    position: absolute;
    width: 16.6666%;
    height: 50px;
    font-size: 40px;
    font-weight: 700;
    line-height: 50px;
    text-align: center;
    @media screen and (max-width: 960px) {
      width: 33.3333%;
      font-size: 30px;
    }
  }
}

.expandArea {
  position: relative;
  border-radius: 50%;
  overflow: hidden;

  &:hover {
    .expandBtn {
      background-color: transparent;
    }
    .btnOverlay {
      right: 0;
    }
  }

  .expandBtn {
    position: relative;
    background-color: rgb(130, 130, 130, 0.3);
    z-index: 1;
    transition: 0.3s;
  }

  .btnOverlay {
    position: absolute;
    top: 0;
    right: -60px;
    width: 60px;
    height: 52px;
    background-image: linear-gradient(to right, black, purple);
    transition: 0.3s;
  }
}
</style>