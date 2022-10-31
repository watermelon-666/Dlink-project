<script>
import PlayAudio from "../components/play-audio.vue";
  export default {
    mixins: [],
    components: {PlayAudio},
    data () {
      let List = [
        {
          title: '热点测试音频1',
          src: 'src/PlayInfo/audio1.mp3',
          adSrc: 'src/PlayInfo/images/inset1.png',
          maxTime: '05:15'
        },
        {
          title: '热点测试音频2',
          src: 'src/PlayInfo/audio2.mp3',
          adSrc: 'src/PlayInfo/images/inset2.png',
          maxTime: '01:34'
        }
      ]
      return {
        infoTitleFlag: 'hotspot', // 默认第一个为“热点”
        contentList: List, // 播放列表（默认为热点数据）
        audioSrc: List[0].src, // 播放地址（默认为热点数据第一条）
        adSrc: List[0].adSrc, // 播放图片地址
        activ: 0 // 选择具体的哪一项
      }
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
            src: 'src/PlayInfo/audio1.mp3',
            adSrc: 'src/PlayInfo/images/inset1.png',
            maxTime: '05:15'
          },
          {
            title: '热点测试音频2',
            src: 'src/PlayInfo/audio2.mp3',
            adSrc: 'src/PlayInfo/images/inset2.png',
            maxTime: '01:34'
          }
        ]
        // 重置地址与高亮显示
        this.audioSrc = this.contentList[0].src
        this.adSrc = this.contentList[0].adSrc
        this.activ = 0
      },
      // 点击理财
      finance () {
        this.infoTitleFlag = 'finance'
        this.contentList = [
          {
            title: '理财测试音频1',
            src: 'src/PlayInfo/audio2.mp3',
            adSrc: 'src/PlayInfo/images/inset2.png',
            maxTime: '01:34'
          },
          {
            title: '理财测试音频2',
            src: 'src/PlayInfo/audio1.mp3',
            adSrc: 'src/PlayInfo/images/inset1.png',
            maxTime: '05:15'
          }
        ]
        this.audioSrc = this.contentList[0].src
        this.adSrc = this.contentList[0].adSrc
        this.activ = 0
      },
      // 点击跨境
      abroad () {
        this.infoTitleFlag = 'abroad'
        this.contentList = [
          {
            title: '跨境测试音频1',
            src: 'src/PlayInfo/audio1.mp3',
            adSrc: 'src/PlayInfo/images/inset1.png',
            maxTime: '05:15'
          },
          {
            title: '跨境测试音频2',
            src: 'src/PlayInfo/audio2.mp3',
            adSrc: 'src/PlayInfo/images/inset2.png',
            maxTime: '01:34'
          }
        ]
        this.audioSrc = this.contentList[0].src
        this.adSrc = this.contentList[0].adSrc
        this.activ = 0
      },
      // 点击基金
      fund () {
        this.infoTitleFlag = 'fund'
        this.contentList = [
          {
            title: '基金测试音频1',
            src: 'src/PlayInfo/audio2.mp3',
            adSrc: 'src/PlayInfo/images/inset2.png',
            maxTime: '01:34'
          },
          {
            title: '基金测试音频2',
            src: 'src/PlayInfo/audio1.mp3',
            adSrc: 'src/PlayInfo/images/inset1.png',
            maxTime: '05:15'
          }
        ]
        this.audioSrc = this.contentList[0].src
        this.adSrc = this.contentList[0].adSrc
        this.activ = 0
      },
      // 点击股市
      stock () {
        this.infoTitleFlag = 'stock'
        this.contentList = [
          {
            title: '股市测试音频1',
            src: 'src/PlayInfo/audio1.mp3',
            adSrc: 'src/PlayInfo/images/inset1.png',
            maxTime: '05:15'
          },
          {
            title: '股市测试音频2',
            src: 'src/PlayInfo/audio2.mp3',
            adSrc: 'src/PlayInfo/images/inset2.png',
            maxTime: '01:34'
          }
        ]
        this.audioSrc = this.contentList[0].src
        this.adSrc = this.contentList[0].adSrc
        this.activ = 0
      },
      // 选择音频
      chooseAudio (item, index) {
        this.audioSrc = item.src
        this.adSrc = item.adSrc
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
          <img style="height: 346px;width: 614px;" :src="adSrc" />
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
          <div class="content-time">{{item.maxTime}}</div>
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
    /* 待定 */
    height: 226px;
  }

  .background {
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
  }

  .page-title .content {
    display: flex;
    height: 100%;
    justify-content: space-between;
    align-items: center;
    z-index: 1;
  }

  .title-text {
    line-height: 50px;
    font-family: HuXiaoBo-NanShen;
    font-size: 48px;
    color: #F9F9F9;
    letter-spacing: 7.35px;
    font-weight: 400;
    margin: 0 108px;
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
    margin: 0 108px;
  }

  .page-content {
    display: flex;
  }

  .play-panel {
    /* height: 762px; */
    width: 44%;
    background: #F9F9F9;
  }

  .panel-poster {
    display: flex;
    justify-content: center;
    padding-top: 72px;
  }

  .audio-icon {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    padding-top: 118px;
  }

  .play-info {
    /* height: 762px; */
    width: 56%;
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
    margin: 72px 0 32px 55px;
    justify-content: space-evenly;
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

  .content-time {
    margin-left: auto;
    margin-right: 32px;
  }

  .title-highlight {
    color: #EC5036;
  }

</style>
