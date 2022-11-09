<template>
  <div class="">
    <!-- section-1  -->
    <v-container :style="{height:'50vh'}" class="mb-60 d-flex align-center">
      <div class="box"></div>
      <div class="box"></div>
      <div class="box"></div>
      <div class="box"></div>
      <div class="box"></div>
      <div class="box"></div>
    </v-container>
    <!-- section-2  -->
    <v-container :style="{height:'50vh'}" class="mb-60 d-flex flex-column ">
      <div class="box2 skyblue"></div>
      <div class="box2"></div>
    </v-container>
    <!-- section-3  -->
    <v-container :style="{height:'50vh'}" class="mb-60 d-flex flex-column ">
      <div class="d-flex mb-3">
        <v-btn v-for="(btn,index) in btnTexts" :key="index" rounded outlined class="mr-3" :class="btn">{{btn}}</v-btn>
        <!-- @click="tweenBoxControl(btn) -->
      </div>
      <div class="box3 gray"></div>
    </v-container>
    <!-- section-4  -->
    <v-container :style="{height:'50vh'}" class="mb-60 ">
      <div class="box4"></div>
      <div class="box5 skyblue"></div>
      <div class="box6 gray"></div>
    </v-container>
    <!-- section-5  -->
    <v-container :style="{height:'50vh'}" class="mb-60 ">
      <div class="box7 translateTest"></div>
    </v-container>
    <!-- section-6  -->
    <v-container :style="{height:'50vh'}" class="mb-60 ">
      <div class="box8 skyblue"></div>
    </v-container>
    <!-- section-7  -->
    <v-container :style="{height:'50vh'}" class="mb-60 ">
      <div class="box9 gray"></div>
    </v-container>
    <!-- section-8  -->
    <v-container :style="{height:'50vh'}" class="mb-60 ">
      <div :style="{borderRadius:'50%'}" class="box10">
      </div>
    </v-container>
    <!-- section-9  -->
    <v-container :style="{height:'50vh'}" class="mb-60 ">
      <div class="box11 gray"></div>
      <div :style="{transform:'translateY(150px)'}" class="box12 skyblue"></div>
    </v-container>

  </div>
</template>

<script>
import { gsap } from 'gsap'
// import { ScrollTrigger } from 'gsap/ScrollTrigger'
export default {
  // name: 'Home',
  components: {},
  data() {
    return {
      btnTexts: ['play', 'pause', 'reverse', 'restart'],
    }
  },
  head: {
    title: 'Home',
  },
  computed: {},
  mounted() {
    // section-8
    // ease
    // power: 基本各種強度的 ease-in ease-out
    // back: 會往前(後)超出預設值
    // elastic: 橡皮筋前後回彈
    // bounce: 彈跳球單向回彈
    // rough: 粗糙雜訊
    // slow: 展示slow motion
    // steps: 階段逐格
    // circ: 二次曲線成長
    // expo: 子數成長
    // sine: 三角函數

    // section-9
    gsap
      .timeline({ repeat: -1 })
      .to('.box11', { duration: 1, borderRadius: '50%', x: 40 })
      .to('.box12', { duration: 1, y: -10 })
      .to('.box12', { duration: 0.3, rotate:45 })
      .to('.box11', { duration: 1,  x: 500 })

    // section-8
    gsap
      .timeline({ repeat: -1 })
      .to('.box10', { duration: 3, x: 200, ease: 'sine.out' }, 'start') // start同時開始
      .to('.box10', { duration: 3, y: 200, ease: 'sine.in' }, 'start') // start同時開始

    // ----------------------------------------

    // ex. 限制範圍 clamp(最小值, 最大值, 輸入值)
    gsap.utils.clamp(0, 100, 105) // returns 100
    gsap.utils.clamp(0, 100, 70) // returns 70
    // 自訂 funciton
    const myFun = gsap.utils.clamp(0, 50)
    myFun(30) // returns 30
    myFun(60) // returns 50
    myFun(-10) // returns 0

    // section7
    const container = gsap.timeline() // 建立時間線
    const first = gsap.to('.box9', { x: 200 }) // 建立動畫1
    const seconde = gsap.to('.box9', { backgroundColor: 'purple', rotate: 45 }) // 建立動畫2

    container.add(first) // 將 Tween 加入 Timeline 內
    container.add(seconde)
    container.getChildren() // 查詢子物件 return [Tween, Tween]
    container.play(0) // 列表動畫從 0秒開始撥放

    // section6
    gsap
      .timeline()
      .to('.box8', { x: 100 })
      .to('.box8', { y: 100 })
      .to('.box8', { x: 200 })
      .to('.box8', { y: 200 })

    // section5
    gsap.to('.box7', {
      duration: 1,
      x: '-=100', // 在預設的css上 再加上動畫
      y: '+=100', // 在預設的css上 再加上動畫
      repeat: -1,
    })

    // section4
    const ani = gsap.timeline() // 會在上一個動畫執行完才執行下一個
    ani
      .to('.box4', {
        duration: 2,
        x: 800,
      })
      .to(
        '.box5',
        {
          duration: 1,
          x: 800,
        },
        '+=1'
      ) // +=1 上一個動畫執行過3秒後 才執行
      .to('.box6', {
        duration: 0.5,
        x: 800,
      })
    // GSDevTools.create(); 要辦會員才可以用

    // section3
    const tween = gsap.to('.box3', {
      duration: 5,
      x: 700,
      ease: 'linear',
      paused: true, // 讓box先靜止
    })

    this.btnTexts.forEach((btnText, index) => {
      const btn = document.querySelector(`.${btnText}`)
      btn.addEventListener('click', () => {
        if (btnText === 'play') tween.play()
        if (btnText === 'pause') tween.pause()
        if (btnText === 'reverse') tween.reverse()
        if (btnText === 'restart') tween.restart()
      })
    })

    // section2
    gsap.fromTo(
      '.box2',
      {
        duration: 1,
        autoAlpha: 0.5, // 效果類似opacity
        // x: 100,
        x: window.innerWidth, // 瀏覽器窗口寬度
        scale: 2,
      },
      {
        duration: 1,
        autoAlpha: 1, // 效果類似opacity
        x: 100,
        scale: 0.5,
        stagger: {
          yoyo: true, // 會讓動畫來回跑 false的話 動畫完成後會瞬間回歸原位
          repeat: -1,
        },
      }
    )

    // section1
    gsap.from('.box', {
      duration: 0.7,
      opacity: 0, // 一開始先透明 慢慢顯示
      y: 'random(500, -500)', // 從上下回來
      // stagger: 0.35, // 錯開時間
      stagger: {
        from: 'center', // start/center/edges/random/end 選擇動畫啟動的順序
        each: 0.35, // 錯開時間
        ease: 'linear',
        // repeat: -1 // 設定 -1 就是無限動畫 寫在裡面代表單個會直接重複執行 不會等全部完成
      },
      repeat: -1, // 整體執行次數
    })
  },
  methods: {
    // tweenBoxControl(type) {
    //   if (type === 'play') this.tween.play()
    //   if (type === 'pause') this.tween.pause()
    //   if (type === 'reverse') this.tween.reverse()
    //   if (type === 'restart') this.tween.restart()
    // },
  },
}
</script>
<style lang="scss" scoped>
.box,
.box2,
.box3,
.box4,
.box5,
.box6,
.box7,
.box8,
.box9,
.box10,
.box11,
.box12,
.box13,
.box14,
.box15 {
  width: 100px;
  height: 100px;
  margin: 10px;
  background-color: pink;
}

.translateTest {
  transform: translate(100px, 100px); // x,y
}

.skyblue {
  background-color: skyblue;
}
.gray {
  background-color: gray;
}
</style>


