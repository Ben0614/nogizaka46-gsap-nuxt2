<template>
  <div class="white--text">
    <!-- section1 -->
    <!-- height的減80px  80px是header的高 (現在因為有在view頁面做判斷 所以不用管) -->
    <div class="section" :style="{backgroundColor:'#000',width:'100%',height:'calc(100vh)',clipPath: 'inset(0)'}">
      <!-- top:'80px' header高 (現在因為有在view頁面做判斷 所以不用管) -->
      <div :style="{position: 'fixed',left: '0',top:'0',width:'100%',height:'100%',zIndex:0}" class="d-flex align-end">
        <!-- 背景影片 -->
        <!-- transform:'rotateY(180deg)' -->
        <video :style="{position:'absolute',width:'100%',top:'0',left:'0'}" src="@/assets/video/2ndAlbum.mp4" autoplay muted loop></video>
        <!-- 文字內容 -->
        <v-container :style="{position:'relative',zIndex:2}" class="d-flex justify-space-between align-end mb-10">
          <div>
            <h1 class="section1Title wow slideInUp text-h1 mb-10" data-wow-duration="0.5s">乃木坂46 新メンバー募集開始</h1>
            <p class="section1Content wow fadeIn text-h5" data-wow-delay="0.7s">
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
          <!-- fn-name 點擊後要調用的function name -->
          <BtnCircle :icon-name="'mdi-chevron-down'" :btn-color="'white'" :btn-hover-color="'gray'" :icon-color="'black'" :icon-hover-color="'white'" :time="'0.3'" :fn-name="'goToSection2'" @goToSection2="goToSection2"></BtnCircle>
          <!-- <v-btn width="50" height="50" icon class="downBtn" @click="goToSection2">
            <v-icon size="30">mdi-chevron-down</v-icon>
          </v-btn> -->
        </v-container>
      </div>
    </div>
    <!-- section2 -->
    <div class="section section2 bg py-10">
      <!-- card -->
      <v-container class="mb-15">
        <h1 class="text-h2 mb-10">私たちの番組</h1>
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
    </div>
    <!-- 卡片側邊欄 -->
    <v-navigation-drawer v-model="drawer" fixed app temporary right width="40%" :style="{zIndex:100}" class="py-5 px-15">
      <v-btn :style="{position:'absolute',top:'20px',right:'20px'}" icon class="black" @click="drawer = false">
        <v-icon color="white">mdi-close</v-icon>
      </v-btn>
      <v-tabs v-model="tab" background-color="transparent" color="black" grow class="mb-5">
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

    <!-- section -->
    <!-- <div class="section bg1">
      <h1 class="text-h1">Route46</h1>
    </div>
    <div class="section bg2">
      <h1 class="text-h1">26th</h1>
    </div>
    <div class="section bg3">
      <h1 class="text-h1">Album</h1>
    </div> -->
  </div>
</template>

<script>
import { WOW } from 'wowjs'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
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
  mounted() {
    // wow
    this.$nextTick(() => {
      // 可以根據不同需求 創建wow
      // offset可以直接在tag裡用data-wow-offset設定
      new WOW({ live: false }).init()
    })
    gsap.registerPlugin(ScrollTrigger)
    
    // 卡片hover和click
    const cards = gsap.utils.toArray('.processCard')
    const cardBtns = gsap.utils.toArray('.processCard .btnCircle')
    const cardBtnIcons = gsap.utils.toArray('.processCard .btnCircle .v-icon')
    cards.forEach((card, index) => {
      // 點擊就打開側邊欄 並指定tab
      card.addEventListener('click', () => {
        this.tab = index
        this.drawer = true
      })
      card.addEventListener('mouseenter', () => {
        gsap.to(cardBtns[index], {
          backgroundColor: '#fff',
        })
        gsap.to(cardBtnIcons[index], {
          color: '#000',
        })
      })
      card.addEventListener('mouseleave', () => {
        gsap.to(cardBtns[index], {
          backgroundColor: 'gray',
        })
        gsap.to(cardBtnIcons[index], {
          color: '#fff',
        })
      })
    })

    // 跑馬燈
    // gsap.utils.toArray 和 document.querySelectorAll 可以通用
    const box = document.querySelector('.box')
    const boxWidth = box.getBoundingClientRect().width
    const boxQuantity = document.querySelectorAll('.box').length
    const totalWidth = boxWidth * boxQuantity
    const marqueeWrapper = document.querySelectorAll('.box')
    const dirFromRight = '-=' + totalWidth

    console.log('boxWidth', boxWidth, 'boxQuantity', boxQuantity)

    const mod = gsap.utils.wrap(0, totalWidth)
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

    const right = gsap
      .timeline({ paused: true })
      .add(marquee(marqueeWrapper, 10, dirFromRight))

    right.play()
  },
  methods: {
    // 到第2區域
    goToSection2() {
      // 80 header高 (現在因為有在view頁面做判斷 所以不用管)
      const top = document.querySelector('.section2').offsetTop
      const scrollToTop = window.setInterval(function () {
        const pos = window.pageYOffset
        if (pos < top) {
          window.scrollTo(0, pos + 20) // 每一次滾動多遠
        } else {
          window.clearInterval(scrollToTop)
        }
      }, 10)
    },
  },
}
</script>

<style lang="scss">
.marquee {
  width: 150%; // width必須大一點 否則有些字會瞬間消失
  height: 50px;
  overflow: hidden;

  @media screen and (max-width: 768px) {
    width: 100%;
  }
}
.marquee .boxes {
  position: relative;
  left: -16.6666%; // 會消除掉的位置
  height: 50px;
}
.marquee .box {
  position: absolute;
  width: 16.6666%;
  height: 50px;
  font-size: 40px;
  font-weight: 700;
  line-height: 50px;
  text-align: center;
}

.section {
  width: 100%;
}

.processCard {
  position: relative;
  height: 600px;
  border: 1px solid gray;
  cursor: pointer;
  overflow: hidden;
  video {
    position: absolute;
    height: 100%;
    top: 0;
    left: 0;
    /* transform: scale(2); */
    z-index: 0;
    opacity: 0;
    transition: 0.3s;
  }
  &:hover video {
    opacity: 1;
    transition: 0.3s;
  }
}

.bg {
  background-color: #0e0e0e;
}

/* .section {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100%;
}

.bg1,
.bg2,
.bg3 {
  background-image: url('@/assets/images//nogizaka46/sub1-3.jpg');
  background-size: cover;
  background-attachment: fixed;
}
.bg2 {
  background-image: url('@/assets/images//nogizaka46/N4627-1200x900-cropped.jpg');
}
.bg3 {
  background-image: url('@/assets/images/nogizaka46/nogizaka46.jpeg');
} */
</style>