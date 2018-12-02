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
        <div class="detail" v-show="showInfo" transition="fade">
            <div class="detail-wrapper clearfix">
                <div class="detail-main">
                    <h1 class="seller-name">{{seller.name}}</h1>
                   <div class="star-wrapper">
                      <star :size="48" :score="seller.score"></star>
                   </div>
                   <div class="seller-title">
                     <div class="line"></div>
                     <div class="text">優惠信息</div>
                     <div class="line"></div>
                   </div>
                   <ul class="supports" v-if="seller.supports">
                     <li class="support-item" v-for="(item,index) in seller.supports" :key="index">
                       <span class="icon" :class="classMap[seller.supports[index].type]"></span>
                       <span class="text">{{seller.supports[index].description}}</span>
                     </li>
                   </ul>
                    <div class="seller-title">
                     <div class="line"></div>
                     <div class="text">商家公告</div>
                     <div class="line"></div>
                   </div>
                   <div class="bulletin">
                     <p class="content">{{seller.bulletin}}</p>
                   </div>
                </div>
            </div>
             <div class="cancel-btn" @click="hideDetail">
                    <i class="icon-close"></i>
            </div>
        </div>
    </div>
</template>
<script>
import star from '../star/star'
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
    },
    hideDetail () {
      this.showInfo = false
    }
  },
  created () {
    //   对应不同的图标，兼容写法
    this.classMap = ['descrease', 'discount', 'guarantee', 'invoice', 'special']
  },
  components: {
    star
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
.clearfix {
    display: inline-block;
}
.clearfix :after {
    display: block;
    content: '';
    height: 0;
    line-height: 0;
    clear: both;
    visibility: hidden;
}
.detail {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 999;
    overflow: auto;
    background-color: rgba(7,17,27, 0.8);
    transition: all 0.8s
}
.detail .fade-transition {
  opacity: 1;
  background: rgba(7,17,27, 0.8)
}
.fade-enter {
  opacity: 0;
  background: rgba(7,17,27, 0)
}
.fade-leave {
  opacity: 0;
  background: rgba(7,17,27, 0)
}
.detail-wrapper {
    min-height: 100%;
    width: 100%;
}
.detail-wrapper .detail-main {
    margin-top: 64px;
    padding-bottom: 64px;
}
.seller-name {
    margin-top: 64px;
    text-align: center;
    font-size: 16px;
    font-weight: 700;
    line-height: 16px;
    color: rgb(255, 255, 255)
}
.cancel-btn {
    margin: -64px auto 0 auto;
    width: 32px;
    height: 32px;
    clear: both;
    position: relative;
    font-size: 32px;
}
.icon-close:before {
  content: "\e903";
}
.star-wrapper {
  margin-top: 18px;
  text-align: center;
  padding: 2px 0;
}
.seller-title {
  display: flex;
  width: 80%;
  margin: 30px auto 24px auto;
}
.line {
  flex: 1;
  position: relative;
  top: -6px;
  border-bottom: 1px solid rgba(255, 255, 255,0.2)
}
.seller-title .text {
  padding: 0 12px;
  font-size: 14px;
  font-weight: 700
}
.supports {
  width: 80%;
  margin: 0 auto;
}
.support-item {
  padding: 0 12px;
  margin-bottom: 12px;
  font-size: 0px;
}
.support-item :last-child {
  margin-bottom: 0;
}
.support-item .icon {
  display: inline-block;
  width: 16px;
  height: 16px;
  vertical-align: top;
  margin-right: 6px;
  background-size: 16px 16px;
  background-repeat: no-repeat;
}
.descrease {
  background-image: url('./decrease_2@2x.png')
}
.discount {
  background-image: url('./discount_2@2x.png')
}
.guarantee {
  background-image: url('./guarantee_2@2x.png')
}
.invoice {
  background-image: url('./invoice_2@2x.png')
}
.special {
  background-image: url('./special_2@2x.png')
}
.support-item .text {
  line-height: 16px;
  font-size: 12px;
}
.bulletin {
  width: 80%;
  margin: 0 auto;
}
.bulletin .content {
  padding: 0 12px;
  line-height: 24px;
  font-size: 12px;
}
</style>
