<script>
  export default {
    mixins: [],
    components: {},
    data () {
      return {
        infoTitleFlag: 'hotspot' // 默认第一个为“热点”
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
      },
      // 点击理财
      finance () {
        this.infoTitleFlag = 'finance'
      },
      // 点击跨境
      abroad () {
        this.infoTitleFlag = 'abroad'
      },
      // 点击基金
      fund () {
        this.infoTitleFlag = 'fund'
      },
      // 点击股市
      stock () {
        this.infoTitleFlag = 'stock'
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
      <div class="play-panel"></div>
      <div class="play-info">
        <div class="info-title">
          <div @click="hotspot" :class="infoTitleFlag==='hotspot'? 'highlight':null">热点</div>
          <div @click="finance" :class="infoTitleFlag==='finance'? 'highlight':null">理财</div>
          <div @click="abroad" :class="infoTitleFlag==='abroad'? 'highlight':null">跨境</div>
          <div @click="fund" :class="infoTitleFlag==='fund'? 'highlight':null">基金</div>
          <div @click="stock" :class="infoTitleFlag==='stock'? 'highlight':null">股市</div>
          <div class="relay"><img style="width: 26px;height: 26px;" src="../images/relay.png"></div>
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
  }

  .page-content {
    display: flex;
  }

  .play-panel {
    height: 762px;
    width: 830px;
    background: #F9F9F9;
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
  }

</style>
