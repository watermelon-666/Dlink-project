<template>
  <div>
    <audio
      ref="audio"
      :src="audioSrc"
      @timeupdate="handleAudioTimeUpdated"
      @loadedmetadata="onLoadedmetadata"
      style="display: none"
      controls></audio>
    <!-- 播放进度条 -->
    <div class="p_slider" @touchstart="handleTouchStart">
      <div class="p_slider_track"></div>
      <div class="p_slider_fill" :style="'width:' + sliderTime + '%'"></div>
      <div class="p_slider_thumb" :style="'left:' + sliderTime + '%'"></div>
    </div>
    <!-- 播放时间 -->
    <div class="play_time">
      <span style="margin-right: 410px">{{realFormatSecond(audio.currentTime)}}</span>
      <span>{{realFormatSecond(audio.maxTime)}}</span>
    </div>
    <!-- 播放按钮 -->
    <div class="audio-icon">
      <div class="last-audio">
        <img style="width: 56px;height: 56px;" src="../images/last-audio.png">
      </div>
      <div @click="playAudio">
        <div class="play-icon" v-if="!audio.playing">
          <img style="width: 80px;height: 80px;" src="../images/playIcon.png">
        </div>
        <div class="play-icon" v-else>
          <img style="width: 80px;height: 80px;" src="../images/bofangzhong@2x.png">
        </div>
      </div>
      <div class="next-audio">
        <img style="width: 56px;height: 56px;" src="../images/next-audio.png">
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      audioSrc: {
        type: String
      }
    },
    data () {
      return {
        sliderTime: 0, //滑动进度时间
        audio: { // 音频播放相关参数
          playing: false, // 音频是否在于播放状态
          maxTime: 0, // 音频最大时长
          currentTime: 0, // 音频当前播放时长
          minTime: 0,
          step: 0.1 // 移动步长
        }
      }
    },
    methods: {
      // 格式化时间
      realFormatSecond(second) {
        var secondType = typeof second

        if (secondType === "number" || secondType === "string") {
          second = parseInt(second)
          var mimute = Math.floor(second / 60)
          second = second - mimute * 60

          return (
            ("0" + mimute).slice(-2) + ":" + ("0" + second).slice(-2)
          )
        } else {
          return "00:00"
        }
      },
      // 控制音频的播放与暂停
      playAudio () {
        console.log('控制音频的播放与暂停')
        this.audio.playing = !this.audio.playing
        return this.audio.playing ? this.$refs.audio.play() : this.$refs.audio.pause()
      },
      // 当指定的音频/视频的元数据已加载时，会发生 loadedmetadata 事件。
      onLoadedmetadata(res) {
        console.log("loadedmetadata数据已加载时")
        this.audio.playing = false
        this.audio.maxTime = parseInt(res.target.duration)
      },
      // 当音频当前时间改变后，进度条也要改变
      handleAudioTimeUpdated(res) {
        // console.log("timeupdate currentTime:", res.target.currentTime)
        this.audio.currentTime = res.target.currentTime
        this.sliderTime = parseInt(
          (this.audio.currentTime / this.audio.maxTime) * 100
        )
      },
      // touchstart	触摸开始，多点触控，后面的手指同样会触发
      // touchmove	接触点改变，滑动时
      // touchend	触摸结束，手指离开屏幕时
      // touchcancel	触摸被取消，当系统停止跟踪触摸的时候触发
      handleTouchStart(e) {
        // console.log(e);
        this.setValue(e.touches[0])
        document.addEventListener("touchmove", this.handleTouchMove)
        document.addEventListener("touchup", this.handleTouchEnd)
        document.addEventListener("touchend", this.handleTouchEnd)
        document.addEventListener("touchcancel", this.handleTouchEnd)
      },
      handleTouchMove(e) {
        // console.log(e.changedTouches[0])
        this.setValue(e.changedTouches[0])
      },
      handleTouchEnd(e) {
        // this.setValue(e.changedTouches[0])
        document.removeEventListener("touchmove", this.handleTouchMove)
        document.removeEventListener("touchup", this.handleTouchEnd)
        document.removeEventListener("touchend", this.handleTouchEnd)
        document.removeEventListener("touchcancel", this.handleTouchEnd)
      },
      // 从点击位置更新 value
      setValue(e) {
        // clientX  点击位置距离当前body可视区域的x，y坐标
        const $el = this.$el
        const { maxTime, minTime, step } = this.audio
        let value =
          ((e.clientX - $el.getBoundingClientRect().left) / $el.offsetWidth) *
          (maxTime - minTime)
        value = Math.round(value / step) * step + minTime
        value = parseFloat(value.toFixed(5))
        if (value > maxTime) {
          value = maxTime
        } else if (value < minTime) {
          value = minTime
        }
        this.$refs.audio.currentTime = value
      },
    }
  }
</script>

<style scoped>
  .p_slider {
    width: 578px;
    position: relative;
    height: 24px;
    display: flex;
    align-items: center;
    margin: 0 126px
  }
  .p_slider_track {
    position: absolute;
    height: 2px;
    left: 0;
    right: 0;
    top: 50%;
    margin-top: -1px;
    background-color: #f6f6f6;
  }

  .p_slider_fill {
    position: absolute;
    height: 2px;
    width: 100%;
    background-color: #CC3729;
    left: 0;
    top: 50%;
    margin-top: -1px;
  }

  .p_slider_thumb {
    position: absolute;
    top: 50%;
    width: 12px;
    height: 12px;
    background-color: #CC3729;
    color: #CC3729;
    border-radius: 50%;
    transform: translate(-50%, -50%);
    cursor: pointer;
  }

  .play_time {
    margin: 30px 126px 0px 126px;
    font-size: 32px;
    color: #111111;
    font-weight: 400;
    letter-spacing: 0;
  }

  .audio-icon {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    padding-top: 77px;
  }
</style>