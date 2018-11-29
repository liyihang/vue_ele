<template>
    <div class="header">
        <div class="content-wrapper">
            <div class="avatar">
                <img width="64" height="64" :src="seller.avatar" alt="">
            </div>
            <div class="content">
                <div class="title">
                    <span class="brand"></span>
                    <span class="name">{{seller.name}}</span>
                </div>
                <div class="description">
                    {{seller.description}}/{{seller.deliveryTime}}分钟送达
                </div>
                <div v-if="seller.supports" class="support">
                    <span class="icon" :class="classMap[seller.supports[0].type]"></span>
                    <span class="text">{{seller.supports[0].description}}</span>
                </div>
            </div>
            <div v-if="seller.supports" class="support-count" @click="showDetail">
                <span class="count">{{seller.supports.length}}个</span>
                <i class="icon-keyboard_arrow_right"></i>
            </div>
        </div>
        <div class="bulletin-wrapper" @click="showDetail" >
            <span class="bulletin-title"></span>
            <span class="bulletin-text">{{seller.bulletin}}</span>
            <i class="icon-keyboard_arrow_right"></i>
        </div>
        <div class="background">
            <img :src="seller.avatar" alt="" width="100%" height="100%">
        </div>
        <div class="detail" v-show="showInfo"></div>
    </div>
</template>
<script>
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      showInfo: false
    }
  },
  methods: {
    showDetail () {
      this.showInfo = true
    }
  },
  created () {
    //   对应不同的图标，兼容写法
    this.classMap = ['descrease', 'discount', 'guarantee', 'invoice', 'special']
  }
}
</script>

<style>
    @import '../../common/css/icon.css';
.header {
    position: relative;
    color: aliceblue;
}
.content-wrapper {
    position: relative;
    padding: 24px 12px 18px 24px;
    font-size: 0
}
.avatar {
    display: inline-block
}
.content {
    display: inline-block;
    margin-left: 16px;
    font-size: 14px;
}
.title {
    margin: 2px 0 8px 0
}
.title .brand {
    vertical-align: top;
    display: inline-block;
    height: 18px;
    width: 30px;
    background-image: url('brand@2x.png');
    background-size: 30px 18px;
    background-repeat: no-repeat
}
.title .brand img {
    border-radius: 6px
}
.title .name {
    margin-left: 6px;
    font-size: 16px;
    font-weight: bold

}
.description {
    font-size: 12px;
    line-height: 12px;
    margin-bottom: 10px;
}
.support .icon {
    display: inline-block;
    width: 16px;
    height: 12px;
    background-size: 12px 12px;
    background-repeat: no-repeat;
    background-image: url('./decrease_1@2x.png')
}
.support .text {
    vertical-align: top;
    font-size: 10px;
    line-height: 12px;
}
.support-count {
    position: absolute;
    right: 12px;
    bottom: 18px;
    padding: 0 8px;
    height: 24px;
    line-height: 24px;
    border-radius: 14px;
    background-color: rgba(0,0,0, 0.2)
}
.count {
    font-size: 10px;
}
.icon-keyboard_arrow_right {
    line-height: 24px;
    font-size: 10px;
    padding-left: 2px;
}
.icon-keyboard_arrow_right:before {
  content: "\e905";
}
.bulletin-wrapper {
    position: relative;
    height: 28px;
    line-height: 28px;
    padding: 0 22px 0 12px;white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    background-color: rgba(7,17,27, 0.2)
}
.bulletin-title {
    vertical-align: top;
    display: inline-block;
    width: 22px;
    height: 12px;
    background-image: url('./bulletin@2x.png');
    background-size: 22px 12px;
    background-repeat: no-repeat;
    margin-top: 8px;
}
.bulletin-text {
    vertical-align: top;
    font-size: 10px;
    margin-top: 4px;

}
.bulletin-wrapper .icon-keyboard_arrow_right {
    position: absolute;
    font-size: 10px;
    right: 12px;
}
.background {
    position:absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    filter: blur(15px)
}
.detail {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 999;
    overflow: auto;
    background-color: rgba(7,17,27, 0.8)
}
</style>
