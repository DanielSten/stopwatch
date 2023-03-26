<template>
  <div class="block_stopwatch" v-bind:class="{ active: isActive }">
    <div class="block_stopwatch-time">{{ formattedTime }}</div>
    <div class="block_stopwatch_btn flex">
      <div class="block_stopwatch_btn-start" v-show="showStartBtn" @click="onStartClick"><i class='bx bx-play' ></i></div>
      <div class="block_stopwatch_btn-pause" v-show="showPauseBtn" @click="onPauseClick"><i class='bx bx-pause' ></i></div>
      <div class="block_stopwatch_btn-stop" @click="onStopClick"><i class='bx bx-stop' ></i></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "stopwatch",
  data() {
    return{
      startTime: null,
      pauseTime: 0,
      returnTime: 0,
      interval: null,
      showStartBtn: true,
      showPauseBtn: false,
      isActive: false
    }
  },
  methods: {
    onStartClick(){
      this.showStartBtn = false
      this.showPauseBtn = true
      this.isActive = true
      this.startTime = Date.now()
      this.interval = setInterval( () => {
        this.returnTime = Date.now() + this.pauseTime - this.startTime
      },100)
    },
    onPauseClick(){
      this.showPauseBtn = false
      this.showStartBtn = true
      this.isActive = false
      this.pauseTime = this.returnTime
      clearInterval(this.interval)
    },
    onStopClick(){
      this.pauseTime = 0
      this.returnTime = 0
      this.isActive = false
      this.showPauseBtn = false
      this.showStartBtn = true
      clearInterval(this.interval)
    },
  },
  computed: {
    formattedTime(){
      let allSeconds = Math.floor(this.returnTime / 1000)
      let seconds = allSeconds % 60
      let allMinutes = (allSeconds - seconds) / 60
      let minutes = allMinutes % 60
      let hours = (allMinutes - minutes) / 60
      let result = String(seconds).padStart(2, '0')
      if(allMinutes > 0){
        result = String(minutes).padStart(2, '0') + ':' + result
      }
      if(hours > 0){
        result = hours + ':' + result
      }
      return result
    },
  }
}
</script>

<style scoped>
.block_stopwatch{
  width: 225px;
  height: 120px;
  background-color: rgba(105, 105, 105, 1);
  margin: 0 25px 45px;
  color: rgba(158, 158, 158, 1);
  text-align: center;

}
.block_stopwatch.active{
  color: white;
}


.flex{
  display: flex;
  justify-content:center;
}
.block_stopwatch-time{
  font-family: 'Gotham Pro', sans-serif;
  margin: 0 auto;
  font-weight: 400;
  font-size: 22px;
  line-height: 21px;
  padding: 20px 0 20px 0;
  border-bottom: 1px solid rgba(158, 158, 158, 1);
}
.bx{
  font-size: 40px;
  line-height: 58px;
  margin: 0 8px;
}
.bx:hover{
  font-size: 40px;
  line-height: 58px;
  margin: 0 8px;
  color: white;
}

</style>