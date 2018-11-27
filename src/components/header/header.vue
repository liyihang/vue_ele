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
        </div>
        <div class="bulletin-wrapper"></div>
    </div>
</template>
<script>
export default {
  props: {
    seller: {
      type: Object
    }
  },
  created () {
    //   对应不同的图标，兼容写法
    this.classMap = ['descrease', 'discount', 'guarantee', 'invoice', 'special']
  }
}
</script>

<style>
.header {
  color: aliceblue;
  background-color: gray
}
.content-wrapper {
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
.icon {
    vertical-align: top;
    display: inline-block;
    width: 12px;
    height: 12px;
    margin-right: 4px;
    background-size: 12px 12px;
    background-repeat: no-repeat;
    background-image: url('./decrease_1@2x.png')
}
.text {
    font-size: 10px;
    line-height: 14px;
}
</style>
