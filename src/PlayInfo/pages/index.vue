<script>
import PlayAudio from "../components/play-audio.vue";
  export default {
    mixins: [],
    components: {PlayAudio},
    data () {
      return {
        infoTitleFlag: 'hotspot', // 默认第一个为“热点”
        contentList: [
          {
            title: '热点测试音频1',
            src: 'src/PlayInfo/audio1.mp3'
          },
          {
            title: '热点测试音频2',
            src: 'src/PlayInfo/audio2.mp3'
          }
        ], // 播放列表（默认为热点数据）
        audioSrc: '', // 播放地址
        activ: '' // 选择具体的哪一项
      }
    },
  
    mounted () {

    },

    methods: {
      // 点击下载事件
      download () {},
      // 点击热点
      hotspot () {
        this.infoTitleFlag = 'hotspot'
        this.contentList = [
          {
            title: '热点测试音频1',
            src: 'src/PlayInfo/audio1.mp3'
          },
          {
            title: '热点测试音频2',
            src: 'src/PlayInfo/audio2.mp3'
          }
        ]
        this.audioSrc = ''
        this.activ = ''
      },
      // 点击理财
      finance () {
        this.infoTitleFlag = 'finance'
        this.contentList = [
          {
            title: '理财测试音频1',
            src: 'src/PlayInfo/audio1.mp3'
          },
          {
            title: '理财测试音频2',
            src: 'src/PlayInfo/audio2.mp3'
          }
        ]
        this.audioSrc = ''
        this.activ = ''
      },
      // 点击跨境
      abroad () {
        this.infoTitleFlag = 'abroad'
        this.contentList = [
          {
            title: '跨境测试音频1',
            src: 'src/PlayInfo/audio1.mp3'
          },
          {
            title: '跨境测试音频2',
            src: 'src/PlayInfo/audio2.mp3'
          }
        ]
        this.audioSrc = ''
        this.activ = ''
      },
      // 点击基金
      fund () {
        this.infoTitleFlag = 'fund'
        this.contentList = [
          {
            title: '基金测试音频1',
            src: 'src/PlayInfo/audio1.mp3'
          },
          {
            title: '基金测试音频2',
            src: 'src/PlayInfo/audio2.mp3'
          }
        ]
        this.audioSrc = ''
        this.activ = ''
      },
      // 点击股市
      stock () {
        this.infoTitleFlag = 'stock'
        this.contentList = [
          {
            title: '股市测试音频1',
            src: 'src/PlayInfo/audio1.mp3'
          },
          {
            title: '股市测试音频2',
            src: 'src/PlayInfo/audio2.mp3'
          }
        ]
        this.audioSrc = ''
        this.activ = ''
      },
      // 选择音频
      chooseAudio (item, index) {
        this.audioSrc = item.src
        this.activ = index
      }
    }
  }

</script>

<template>
  <div class="page">
    <div class="page-title">
      <div class="content">
        <div class="title-text">中银资讯</div>
        <div class="title-download" @click="download">下载APP</div>
      </div>
      <img class="background" src="../images/background.png">
    </div>
    <div class="page-content">
      <div class="play-panel">
        <!-- 播放海报/广告处 -->
        <div class="panel-poster">
          <!-- 此处应为海报/广告链接 先以黑色矩形块替代 -->
          <div style="height: 346px;width: 614px;background: #000;" />
        </div>
        <play-audio style="margin-top: 53px;" :audioSrc="audioSrc" />
      </div>

      <div class="play-info">
        <div class="info-title">
          <div @click="hotspot" :class="infoTitleFlag==='hotspot'? 'highlight':null">热点</div>
          <div @click="finance" :class="infoTitleFlag==='finance'? 'highlight':null">理财</div>
          <div @click="abroad" :class="infoTitleFlag==='abroad'? 'highlight':null">跨境</div>
          <div @click="fund" :class="infoTitleFlag==='fund'? 'highlight':null">基金</div>
          <div @click="stock" :class="infoTitleFlag==='stock'? 'highlight':null">股市</div>
          <div class="relay"><img style="width: 26px;height: 26px;" src="../images/relay.png"></div>
          <div class="switch"><img style="width: 25px;height: 26px;" src="../images/switch.png"></div>
        </div>
        <div class="info-content" v-for="(item,index) in contentList" :key="index">
          <div class="icon-normal"><img style="width: 41px;height: 41px;" src="../images/bofang01.png"></div>
          <div class="content-title" :class="index === activ ? 'title-highlight' : ''" @click="chooseAudio(item, index)">{{item.title}}</div>
          <div>4:20</div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .page {
    height: 100%;
    width: 100%;
    background: #f6f7f6;
    overflow-y: auto;
  }

  .page-title {
    height: 126px;
    position: relative;
  }

  .background {
    height: 126px;
    width: 100%;
  }

  .page-title .content {
    display: flex;
    position: absolute;
  }

  .title-text {
    line-height: 50px;
    font-family: HuXiaoBo-NanShen;
    font-size: 48px;
    color: #F9F9F9;
    letter-spacing: 7.35px;
    font-weight: 400;
    margin: 38px 108px;
    z-index: 1;
  }

  .title-download {
    width: 153px;
    height: 49px;
    line-height: 45px;
    font-family: PingFangSC-Regular;
    font-size: 25.92px;
    color: #F9F9F9;
    letter-spacing: 3.97px;
    font-weight: 400;
    border: 2px solid #F9F9F9;;
    border-radius: 144px;
    text-align: center;
    margin: 38px 0 38px 980px;
    z-index: 1;
  }

  .page-content {
    display: flex;
  }

  .play-panel {
    height: 762px;
    width: 830px;
    background: #F9F9F9;
  }

  .panel-poster {
    margin: 72px 108px 0 108px;
  }

  .audio-icon {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    padding-top: 118px;
  }

  .play-info {
    height: 762px;
    width: 1090px;
    background: #FFF;
  }

  .info-title {
    opacity: 0.65;
    font-family: PingFangSC-Regular;
    font-size: 30px;
    color: #1D2329;
    letter-spacing: 0;
    text-align: center;
    font-weight: 400;
    display: flex;
    margin: 72px 117px 32px 55px;
  }

  .info-title>div{
    width: 135px;
    height: 68px;
    line-height: 68px;
  }

  .info-title .highlight {
    height: 68px;
    width: 145px;
    line-height: 60px;
    border: 4px solid #EC5036;
    border-radius: 200px;
  }

  .info-title .relay {
    /* height: 26px; */
    width: 22px;
    margin-left: 86px;
  }

  .info-title .switch {
    width: 26px;
    margin-left: 90px;
  }

  .info-content {
    display: flex;
    width: 100%;
    height: 103px;
    font-size: 32px;
    color: #919193;
    letter-spacing: 0;
    line-height: 103px;
    font-weight: 400;
    margin-bottom: 18.6px;
  }

  .icon-normal {
    margin: 11px 30px 31px 55px;
  }

  .content-title {
    width: 771px;
  }

  .title-highlight {
    color: #EC5036;
  }

</style>
