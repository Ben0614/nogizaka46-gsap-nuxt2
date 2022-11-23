<template>
  <div>
    <!-- section-1  -->
    <div :style="{padding:isMobile ? '80px 50px 50px' : '400px 50px 50px'}" class="white mb-60 d-flex justify-space-between" :class="isMobile ? 'flex-column align-start' : 'align-end'">
      <h1 class="fade-up font-weight-bold" :class="isMobile ? 'text-h3 mb-3' : 'text-h1'">
        乃木坂46は
        <br>
        未来です
      </h1>
      <h4 class="fade-up font-weight-bold" :class="isMobile ? 'text-h6' : 'text-h4'">僕は信じます</h4>
    </div>

    <!-- video 伸縮 -->
    <div :style="{position:'relative',margin:'0 0 300px'}" class="d-flex justify-center">
      <div ref="videoWrap" :style="{position:'relative',width:'95%',borderRadius:'10px',overflow:'hidden'}">
        <!-- 影片區域 -->
        <!-- objectFit:'cover' 對圖片進行剪切，保留原始比例 -->
        <video :style="{width:'100%',height:isMobile ? '100vh' : '100%',objectFit:'cover'}" autoplay muted loop src="@/assets/video/22nd.mp4"></video>
        <!-- 黑色遮罩 -->
        <div class="video-bg"></div>
        <!-- 文字內容區域 -->
        <div :style="{position:'absolute',top:isMobile ? '0' : isNoteBook ? '10%' : '15%',left:isMobile ? '0' : isNoteBook ? '0' : '20%',zIndex:'2',width:'800px',maxWidth:'100%'}" class="white--text mx-auto pa-10">
          <h2 class="fade-up mb-3" :class="isMobile ? 'text-h5' : isNoteBook ? 'text-h4' : 'text-h3'">
            乃木坂46
          </h2>
          <h4 class="fade-up" :class="isMobile ? 'mb-10' : isNoteBook ? 'text-h5 mb-5': 'text-h4 mb-15'">のぎざか フォーティーシックス</h4>
          <p class="fade-up" :class="isMobile ? '' : isNoteBook ? 'text-body-1' : 'text-h6'">日本の女性アイドルグループである。秋元康のプロデュースにより、2011年8月21日に結成した</p>
          <p class="fade-up" :class="isMobile ? '' : isNoteBook ? 'text-body-1' : 'text-h6'">2011年にソニー・ミュージックエンタテインメント (SME) と秋元康の合同プロデュースによる新たな女性アイドルグループが企画され、乃木坂46の結成に至った。</p>
          <p class="fade-up mb-10" :class="isMobile ? '' : isNoteBook ? 'text-body-1' : 'text-h6'">
            乃木坂46はAKB48グループに所属せず、AKB48の公式ライバルとして存在する[7]。AKB48グループが専用劇場を持つのに対し、乃木坂46は専用劇場を持たない[7]。AKB48グループが選抜総選挙を実施するのに対し、乃木坂46は舞台『16人のプリンシパル』における配役決定で投票を実施するという差別化を図っている[8]。このような差別化は乃木坂46の1stシングル『ぐるぐるカーテン』のミュージック・ビデオ (MV) における私立女子校の風景から提示され始めた[9]。
          </p>
          <BtnNormal class="fade-up" :content="'Nogizaka46'" :btn-color="'#fff'" :text-color="'#fff'" :text-hover-color="'#000'" :circle-color="'#fff'" :time="'0.3'" />
        </div>
      </div>
      <!-- play按鈕 -->
      <div class="playCirclePosition">
        <PlayCircle :dialog-visible="dialogVideo" :youtube-path="'https://www.youtube.com/embed/QaGgbf_VNR4'" @openVideo="openVideo" @dialogClose="closeDialog" />
      </div>
    </div>

    <!-- 圓球背景 -->
    <div ref="circleWrap" :style="{margin:'0 0 100px',position:'relative'}" class="d-flex justify-center pb-15">
      <!-- 圓球 -->
      <div ref="greyCircle" :style="{position:'absolute',top:'0',zIndex:'2',background:'gray',width:'0',height:'0',borderRadius:'50%'}"></div>
      <!-- 圖片外層 -->
      <div :style="{position:'relative',margin:'400px 0 60px',width:isMobile ? '100%' : '80%'}" class="d-flex justify-center">
        <!-- 圖片區域 -->
        <v-img :style="{position:'relative',zIndex:'2'}" :src="require('@/assets/images/nogizaka46/nogizaka46.jpeg')" class="fade">
          <!-- 圖片遮罩 -->
          <div class="img-bg"></div>
          <!-- 文字內容區域 -->
          <div :style="{position:'relative',zIndex:'1',width:'800px',maxWidth:'100%'}" class="white--text mx-auto py-15 px-3">
            <h2 class="fade-up text-h3 mb-15">
              乃木坂46
            </h2>
            <p class="fade-up text-h6">日本大型女子偶像團體，成立於2011年8月21日；其出道時定位為另一女子偶像團體AKB48的「官方對手」（公式ライバル），但有獨立的幕後團隊，行銷策略及團體風格也與AKB48系列團體不同，惟總製作人同樣是秋元康。目前共有43名成員，其中隊長為秋元真夏、副隊長為梅澤美波。</p>
            <p class="fade-up text-h6">乃木坂46最初是做為「AKB48官方對手」而成立的女子團體。與AKB48及其姊妹團體（如SKE48等）不同，舉行公演時並不擁有專屬表演場地（如AKB48劇場），但操作方式較為專業。根據秋元康所說，團體名稱中的「46」象徵「就算人數比AKB48少，也具有不遜於AKB48的幹勁」。</p>
            <p class="fade-up text-h6 mb-10">
              乃木坂46全體成員所屬的經紀公司為「乃木坂46合同會社」（乃木坂46LLC）。附屬於乃木坂46合同會社的「乃木坂46營運委員會」（乃木坂46運営委員会）負責整個團體的營運工作。
            </p>
            <BtnNormal class="fade-up" :content="'Nogizaka46'" :btn-color="'#fff'" :text-color="'#fff'" :text-hover-color="'#000'" :circle-color="'#fff'" :time="'0.3'" />
          </div>
        </v-img>
        <!-- play按鈕 -->
        <div class="playCirclePosition">
          <PlayCircle :dialog-visible="dialogVideo2" :youtube-path="'https://www.youtube.com/embed/rUTlSUQCMuo'" @dialogClose="closeDialog" @openVideo="openVideo2" />
        </div>
      </div>

    </div>

    <!-- card -->
    <v-container class="mb-10">
      <div class="d-flex justify-space-between" :class="isMobile ? 'flex-column' : ''">
        <!-- 幫每個card動態添加class card+index -->
        <div v-for="(card,index) in cardData" :key="index" class="fade-up myCard rounded" :class="`card${index}`" @mouseenter="showCard(`card${index}`)" @mouseleave="closeCard(`card${index}`)" @click="openPage(card.link)">
          <v-img class="cardImg" width="100%" height="100%" :src="card.img"></v-img>
          <div :style="{height:'100%'}" class="cardText">
            <div class="title">
              <h3>{{card.title}}</h3>
              <p>{{card.subTitle}}</p>
            </div>
            <p class="content">{{card.content}}</p>
          </div>
          <div class="linkIcon">
            <v-icon>mdi-link-variant</v-icon>
          </div>
        </div>
      </div>
    </v-container>

    <!-- join -->
    <div ref="joinArea" :style="{backgroundColor:'#000',cursor: 'pointer',padding:'100px 0'}" class="joinArea white--text mb-15" @click="goToPage('detail')">
      <p class="text-center mb-5">オーディション</p>
      <h1 class="text-h1 text-center mb-10">Join Us!</h1>
      <div class="d-flex justify-center">
        <BtnNormal ref="joinBtn" class="joinBtn" :content="'募集一覧 / 応募'" :btn-color="'#fff'" :text-color="'#fff'" :text-hover-color="'#9e3eb2'" :circle-color="'#fff'" :time="'0.3'" />
      </div>
    </div>

  </div>
</template>

<script>
// import AOS from 'aos'
// import { WOW } from 'wowjs'
// import GSDevTools from "gsap/GSDevTools"
import BtnNormal from '@/components/base/BtnNormal'
import PlayCircle from '@/components/PlayCircle'
export default {
  name: 'Home',
  components: {
    BtnNormal,
    PlayCircle,
  },
  data() {
    return {
      dialogVideo: false,
      dialogVideo2: false,
      cardData: [
        {
          title: 'Route246',
          subTitle: '2020/7/24',
          content:
            '合乃木坂46的第3首數位下載限定歌曲，於2020年7月24日由N46Div.推出。',
          img: require('@/assets/images/nogizaka46/sub1-3.jpg'),
          link: 'https://www.youtube.com/watch?v=2J5EQQ9eozE&ab_channel=gba2001',
        },
        {
          title: '僕は僕を好きになる',
          subTitle: '2021/1/27',
          content:
            '乃木坂46的第26張單曲，由秋元康作詞、杉山勝彥作曲。2021年1月27日由N46Div.發行。同名標題曲的Center（中心成員）由山下美月擔任',
          img: require('@/assets/images/nogizaka46/N4627-1200x900-cropped.jpg'),
          link: 'https://www.youtube.com/watch?v=F_WgREJgJhw&ab_channel=%E4%B9%83%E6%9C%A8%E5%9D%8246OFFICIALYouTubeCHANNEL',
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
    // 如果從其他頁非頂部跳轉 到新頁面的pageYOffset會跟前一頁一樣
    // 這會造成scrollTrigger start end產生問題
    window.scrollTo(0, 0)
    console.log('Home window.pageYOffset',window.pageYOffset);
    // aos
    // AOS.init()
    // wow
    // new WOW({ live: false }).init()

    // fadeUp
    const fadeUps = this.$gsap.utils.toArray('.fade-up')
    fadeUps.forEach((fadeUp, index) => {
      this.$gsap.from(fadeUp, {
        scrollTrigger: {
          trigger: fadeUp,
        },
        y: 100,
        opacity: 0,
      })
    })
    // fade
    this.$scrollTrigger.matchMedia({
      '(min-width: 0px) and (max-width: 959px)': () => {
        this.$gsap.from('.fade', {
          scrollTrigger: {
            trigger: '.fade',
            start: 'center bottom',
            // markers: true,
          },
          opacity: 0,
          duration: 3,
        })
      },
      '(min-width: 960px)': () => {
        this.$gsap.from('.fade', {
          scrollTrigger: {
            trigger: '.fade',
            start: 'center center+=200',
            // markers: true,
          },
          opacity: 0,
          duration: 3,
        })
      },
    })

    // video和circle
    // 如果需要設斷點 就用matchMedia
    // 不用設斷點 就直接寫gsap.to即可
    // markers 開啟的狀態下 跳到別頁畫面可能會有點偏移 F5重整或關閉markers即可
    this.$scrollTrigger.matchMedia({
      // 跟設定css一樣  如果畫面不小於 0px 執行
      '(min-width: 0px)': () => {
        // video
        // this.$refs.videoWrap 要變化得物件
        this.$gsap.to(this.$refs.videoWrap, {
          // x: 300,
          // rotation: 360,
          duration: 1,
          width: '100%',
          borderRadius: '0px',
          scrollTrigger: {
            trigger: this.$refs.videoWrap, // 觸發得物件
            start: 'top +=50%', // (物件開始位置, 卷軸(變化)開始位置) top center bottom px
            end: '+=50%', // (物件結束位置, 卷軸(變化)結束位置)
            pin: false, // 物件執行完動畫會跟著卷軸走，類似 fixed-top
            scrub: true, // 物件動畫根據卷軸捲動程度跑
            // markers: true, // 顯示標記
          },
        })
        // circle
        // 這個會造成爆版 而且還會有bug 必須要在這個頁面最外層放overflow hidden解決
        this.$gsap.to(this.$refs.greyCircle, {
          width: '200px',
          height: '200px',
          scale: 50,
          scrollTrigger: {
            trigger: this.$refs.greyCircle,
            start: 'top +=50%', // (物件開始位置, 卷軸開始位置) top center bottom px
            end: '+=50%', // (物件結束位置, 卷軸結束位置)
            pin: false,
            scrub: true,
            // markers: true,
          },
        })
        this.$gsap.to(this.$refs.circleWrap, {
          overflow: 'hidden',
          scrollTrigger: {
            trigger: this.$refs.circleWrap,
            start: 'top top-=200', // (物件開始位置, 卷軸開始位置) top center bottom px
            end: 'top', // (物件結束位置, 卷軸結束位置)
            pin: false,
            scrub: true,
            // markers: true,
          },
        })
      },
    })

    // join
    // vuetify的class是important 會造成gsap無法覆蓋
    // css的:hover必須用深層寫法才能改變component的class 所以這裡先用gsap
    const joinArea = document.querySelector('.joinArea')
    const joinBtnCircle = document.querySelector(
      '.joinBtn > span > .btn-circle'
    )
    const joinBtnText = document.querySelector('.joinBtn > span > .btn-text')
    console.log('joinBtnCircle', joinBtnCircle)
    console.log('joinBtnText', joinBtnText)
    // ref獲取法 較為麻煩
    // const joinArea = this.$refs.joinArea
    // const joinBtnCircle = this.$refs.joinBtn.$el.childNodes[0].childNodes[0]
    // const joinBtnText = this.$refs.joinBtn.$el.childNodes[0].childNodes[2]
    // console.log('joinBtnCircle',joinBtnCircle);
    // console.log('joinBtnText',joinBtnText);
    joinArea.addEventListener('mouseenter', () => {
      this.$gsap.to(joinArea, {
        duration: 0.3,
        backgroundColor: '#9e3eb2',
      })
      this.$gsap.to(joinBtnCircle, {
        duration: 0.1,
        scale: 50,
      })
      this.$gsap.to(joinBtnText, {
        duration: 0.3,
        color: '#9e3eb2',
      })
    })
    joinArea.addEventListener('mouseleave', () => {
      this.$gsap.to(joinArea, {
        duration: 0.3,
        backgroundColor: '#000',
      })
      this.$gsap.to(joinBtnCircle, {
        duration: 0.1,
        scale: 1,
      })
      this.$gsap.to(joinBtnText, {
        duration: 0.3,
        color: '#fff',
      })
    })

    //   const siblingsLeft = cards.slice(index + 1)
    //   const siblingsRight = cards.slice(0, index)
  },
  methods: {
    openVideo(val) {
      this.dialogVideo = val
    },
    openVideo2(val) {
      this.dialogVideo2 = val
    },
    closeDialog(val) {
      this.dialogVideo = val
      this.dialogVideo2 = val
    },
    // 觸碰到card
    showCard(cardClass) {
      // 手機版不做改變
      if (this.isMobile) return
      // 獲取card和底下的子元素
      const card = document.querySelector(`.${cardClass}`)
      const cardImg = document.querySelector(`.${cardClass} > .cardImg`)
      const cardTitle = document.querySelector(
        `.${cardClass} > .cardText > .title`
      )
      const cardContent = document.querySelector(
        `.${cardClass} > .cardText > .content`
      )
      const linkIcon = document.querySelector(`.${cardClass} > .linkIcon`)
      // 獲取其他卡片
      const p = card.parentNode.children

      // 卡片寬度
      card.style.width = 'calc(80% - 10px)'
      // 卡片圖片顯示
      cardImg.style.opacity = 1
      // 標題顏色
      cardTitle.style.color = '#fff'
      // 文字內容顯示
      cardContent.style.opacity = 1
      // icon背景色
      linkIcon.style.backgroundColor = 'rgba(236, 236, 236,0.3)'
      // 其他卡片寬度修改
      p.forEach((children, i) => {
        if (children !== card) {
          children.style.width = 'calc(20% - 10px)'
        }
      })

      // console.log('card', card)
      // console.log('cardImg', cardImg)
      // console.log('p', p)
    },
    // 從card移開
    closeCard(cardClass) {
      if (this.isMobile) return
      // 獲取card和底下的子元素
      const card = document.querySelector(`.${cardClass}`)
      const cardImg = document.querySelector(`.${cardClass} > .cardImg`)
      const cardTitle = document.querySelector(
        `.${cardClass} > .cardText > .title`
      )
      const cardContent = document.querySelector(
        `.${cardClass} > .cardText > .content`
      )
      const linkIcon = document.querySelector(`.${cardClass} > .linkIcon`)
      // 獲取其他卡片
      const p = card.parentNode.children

      // 卡片寬度
      card.style.width = 'calc(50% - 10px)'
      // 卡片圖片顯示
      cardImg.style.opacity = 0.3
      // 標題顏色
      cardTitle.style.color = '#000'
      // 文字內容顯示
      cardContent.style.opacity = 0.3
      // icon背景色
      linkIcon.style.backgroundColor = 'rgba(236, 236, 236,1)'
      // 其他卡片寬度修改
      p.forEach((children, i) => {
        if (children !== card) {
          children.style.width = 'calc(50% - 10px)'
        }
      })
    },
    // 開啟卡片連結
    openPage(link) {
      const a = document.createElement('a')
      a.href = link
      a.target = '_blank'
      a.click()
    },
    goToPage(pageName) {
      this.$router.push({ name: pageName })
    },
    // videoControl() {
    //   console.log('元素離頂部高度', this.$refs.videoWrap.offsetTop)
    //   console.log('元素本身高度', this.$refs.videoWrap.offsetHeight)
    //   console.log('視窗高度', window.innerHeight)
    //   console.log('滾動距離', window.pageYOffset)
    // },
  },
}
</script>
<style lang="scss" scoped>
.video-bg,
.img-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  z-index: 0;
}

.myCard {
  position: relative;
  width: calc(50% - 10px);
  height: 500px;
  border: 1px solid #000;
  transition: 0.3s;
  cursor: pointer;

  @media screen and (max-width: '960px') {
    width: 100%;
    margin: 0 0 10px;
  }

  .cardImg {
    position: absolute;
    opacity: 0.3;
    transition: 0.3s;
    z-index: 0;
    @media screen and (max-width: '960px') {
      opacity: 1;
    }
  }
  .cardText {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 40px;

    .title {
      transition: 0.3s;
    }
    .content {
      color: #fff;
      opacity: 0;
      transition: 0.3s;
      width: 80%;
      @media screen and (max-width: '960px') {
        opacity: 1;
      }
    }
  }
  .linkIcon {
    position: absolute;
    bottom: 50px;
    right: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 80px;
    height: 80px;
    border-radius: 50%;
    background-color: rgba(236, 236, 236, 1);
    transition: 0.3s;
    @media screen and (max-width: '960px') {
      bottom: 20px;
      right: 20px;
    }
  }
}
.playCirclePosition {
  position: absolute;
  z-index: 2;
  bottom: -80px;
  right: 100px;
  @media screen and (max-width: '960px') {
    right: 20px;
  }
}
</style>


