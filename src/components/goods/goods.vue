<template>
    <div class="goods-wrapper">
        <div class="menu-wrapper" ref="menuWrapper">
          <ul>
            <li v-for="(item,index) in goods" :key="index" class="menu-item" :class="{'current':currentIndex==index}" @click="selectMenu(index)">
              <span class="text">
                <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>{{item.name}}
                </span>
            </li>
          </ul>
        </div>
        <div class="food-wrapper" ref="foodWrapper">
          <ul>
            <li v-for="(item,index) in goods" :key="index" class="food-list food-list-hook" ref="foodList">
              <h1 class="title">{{item.name}}</h1>
              <ul>
                <li v-for="(food,index) in item.foods" :key="index" class="food-item">
                  <div class="img">
                    <img height="57" width="57" :src="food.icon" alt="">
                  </div>
                  <div class="content">
                    <h2 class="name">{{food.name}}</h2>
                    <p class="desc">{{food.descprition}}</p>
                    <div class="extra">
                      <span class="sellerCount">月售{{food.sellCount}}份</span>
                      <span>好评率{{food.rating}}%</span>
                    </div>
                    <div class="price">
                      <span class="new">￥{{food.price}}</span>
                      <span  class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                    </div>
                  </div>
                </li>
              </ul>
            </li>
          </ul>
        </div>
        <cart></cart>
    </div>
</template>
<script>
import BScroll from 'better-scroll'
import cart from '../cart/cart'
const ERROK = 0
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      goods: [],
      listHeight: [],
      scrollY: 0
    }
  },
  components: {
    cart
  },
  created () {
    //   对应不同的图标，兼容写法
    this.classMap = ['descrease', 'discount', 'guarantee', 'invoice', 'special']
    this.axios.get('/api/goods').then((response) => {
      response = response.data
      if (response.errno === ERROK) {
        this.goods = response.data
        this.$nextTick(() => {
          this._scrollInit()
          this._calculateHeight()
        })
      }
    })
  },
  computed: {
    // 计算当前索引位置
    currentIndex () {
      for (let i = 0; i < this.listHeight.length; i++) {
        let height1 = this.listHeight[i]
        let height2 = this.listHeight[i + 1]
        if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
          return i
        }
      }
      return 0
    }
  },
  methods: {
    // 菜单分类选择
    selectMenu (index) {
      let foodList = this.$refs.foodList
      let el = foodList[index]
      this.foodScroll.scrollToElement(el, 300)
    },
    _scrollInit () {
      // 没有传递click 和type参数
      this.menuScroll = new BScroll(this.$refs.menuWrapper, {
        click: true
      })
      this.foodScroll = new BScroll(this.$refs.foodWrapper, {
        click: true,
        probeType: 3
      })
      this.foodScroll.on('scroll', (pros) => {
        this.scrollY = Math.abs(Math.round(pros.y))
      })
    },
    // 计算高度
    _calculateHeight () {
      let foodList = this.$refs.foodList
      let height = 0
      this.listHeight.push(height)
      for (let i = 0; i < foodList.length; i++) {
        let item = foodList[i]
        height += item.clientHeight
        this.listHeight.push(height)
      }
    }
  }
}
</script>

<style>
.goods-wrapper {
    display: flex;
    position: absolute;
    width: 100%;
    top: 174px;
    bottom: 46px;
    overflow: hidden;
}
.menu-wrapper {
    flex: 0 0 80px;
    width: 80px;
    background:#f3f5f7;
}
.menu-item {
  display: table;
  height: 54px;
  width: 56px;
  line-height: 14px;
  padding: 0 12px;
}
.icon {
  display: inline-block;
  width: 12px;
  height: 12px;
  vertical-align: top;
  margin-right: 2px;
  background-size: 12px 12px;
  background-repeat: no-repeat;
}
.descrease {
  background-image: url('./decrease_3@3x.png')
}
.discount {
  background-image: url('./discount_3@3x.png')
}
.guarantee {
  background-image: url('./guarantee_3@3x.png')
}
.invoice {
  background-image: url('./invoice_3@3x.png')
}
.special {
  background-image: url('./special_3@3x.png')
}
.menu-item .text {
  display: table-cell;
  width: 56px;
  vertical-align: middle;
  font-size: 12px;
  border-bottom: 1px solid rgba(7, 17, 27,0.1)
}
.current {
  position: relative;
  margin-top: 1px;
  z-index: 10;
  background: #fff;
  font-weight: 700
}
.current .text {
  border: none
}
.food-wrapper {
  flex:1
}
.food-wrapper .title {
  padding-left: 14px;
  height: 26px;
  line-height: 26px;
  border-left: 2px solid #d9dde1;
  font-size: 12px;
  color: rgb(147,153,159);
  background: #f3f5f7;
}
.food-item {
  display: flex;
  margin: 18px;
  padding-bottom: 18px;
  border-bottom: 1px solid rgba(7, 17, 27,0.1);
}
.food-item :last-child {
  border: none;
  margin-bottom: 0;
}
.food-item .img {
  flex: 0 0 57px;
  margin-right: 10px;
}
.food-item .content {
  flex: 1;
}
.food-item .name {
  margin: 2px 0 8px 0;
  height: 14px;
  line-height: 14px;
  font-size: 14px;
  color: rgb(7, 17, 27)
}
.extra {
  margin-top: 8px;
}
.extra,.desc {
  font-size: 10px;
  line-height: 10px;
  color: rgb(147,153,159)
}
.desc {
  line-height: 10px;
}
.sellerCount {
  padding-right: 12px;
}
.price {
  font-weight: 700;
  line-height: 24px;
}
.price .new {
  margin-right: 8px;
  font-size: 14px;
  color: rgb(240, 20, 20)
}
.price .old {
  text-decoration: line-through;
  font-size: 10px;
  color:rgb(147,153,159);
}
</style>
