<template>
  <section class="container">
    <h1 class="title">10秒で何回タップできるか</h1>
    <button class="btn-tap" :disabled="timer <= 0 || timer == 10000" @click="addCount">
      <span>{{ count }}</span><br>タップ!!
    </button>
    <div>残り時間 {{ timer / 1000 }} 秒</div>
    <div class="btnArea" v-if="!isPlaying">
      <button class="btn" v-if="timer == 10000" @click="startGame">start</button>
      <button class="btn" v-if="timer <= 0" @click="resetGame">もう一回</button>
      <button class="btn-tw" v-if="timer <= 0" @click="shareTw">記録をつぶやく</button>
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      count: 0,
      timer: 10000,
      isPlaying: false
    }
  },

  methods: {
    addCount() {
      if (this.timer > 0) this.count++
    },

    countDown() {
      this.timer-=100
      this.startGame()
    },

    startGame() {
      this.isPlaying = true
      setTimeout( () => {
        if (this.timer > 0) {
          this.countDown()
        } else {
          this.isPlaying = false
        }
      }, 100)
    },

    resetGame() {
      this.count = 0
      this.timer = 10000
      this.startGame()
    },

    shareTw() {
      const text = encodeURIComponent('10秒間で' + this.count + '回タップしました')
      const hashtags = encodeURIComponent('10秒で何回タップできるか')
      const url = encodeURIComponent('https://tap10s.web.app/')
      const payload = `text=${text}&hashtags=${hashtags}&url=${url}`
      window.open('https://twitter.com/intent/tweet?' + payload, '_blank');
    },
  }
}
</script>

<style>
html {
  touch-action: manipulation;
}
.container {
  padding: 15px;
  text-align: center;
  font-size: 16px;
}
.title {
  font-size: 20px;
  margin-top: 10px;
  margin-bottom: 20px;
}
.btn-tap {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    color: #fff;
    background-color: #a0ce00;
    border: none;
    font-size: 20px;
    margin-bottom: 30px;
}
.btn-tap:disabled {
  background-color: #ddd;
  color: #aaa;
}
.btn-tap span {
  font-size: 60px;
}
.btnArea {
  margin-top: 30px;
}
.btn {
  width: 100%;
  display: inline-block;
  padding: 10px;
  border: none;
  border-radius: 10px;
  background-color: #54bbc1;
  font-size: 18px;
  color: #fff;
  margin: 10px 0;
  text-decoration: none;
  text-align: center;
  font-weight: bold;
  cursor: pointer;
}
.btn-tw {
  width: 100%;
  display: inline-block;
  padding: 10px;
  border: none;
  border-radius: 10px;
  background-color: #54bbc1;
  font-size: 18px;
  color: #fff;
  margin: 10px 0;
  text-decoration: none;
  text-align: center;
  font-weight: bold;
  cursor: pointer;
  background-color: #46a1eb;
}
</style>
