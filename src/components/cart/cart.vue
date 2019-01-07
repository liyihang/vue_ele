<template>
<div class="shopcart">
    <div class="cart-content">
        <div class="content-left">
            <div class="logo-wrapper">
            <div class="logo" :class="{'light':totalCount>0}">
                <i class="icon-shopping_cart" :class="{'light':totalCount>0}"></i>
            </div>
            <div class="num" v-show="totalCount>0">{{totalCount }}</div>
        </div>
        <div class="price" :class="{'highlight':totalCount>0}">￥{{totalPrice}}</div>
        <div class="deliver">另需配送费{{deliveryPrice}}￥</div>
        </div>
        <div class="content-right">
            <div class="pay" :class="payClass">{{priceDesc}}</div>
        </div>
    </div>
</div>
</template>
<script>
export default {
  props: {
    selectFoods: {
      type: Array,
      default () {
        return [
          {
            price: 0,
            count: 0
          }
        ]
      }
    },
    deliveryPrice: {
      type: Number,
      default: 0
    },
    minPrice: {
      type: Number,
      count: 0
    }
  },
  computed: {
    totalPrice () {
      let total = 0
      this.selectFoods.forEach(food => {
        total += food.price * food.count
      })
      return total
    },
    totalCount () {
      let count = 0
      this.selectFoods.forEach(food => {
        count += food.count
      })
      return count
    },
    priceDesc () {
      if (this.totalPrice === 0) {
        return `￥${this.minPrice}员起送`
      } else if (this.totalPrice < this.minPrice) {
        let diff = this.minPrice - this.totalPrice
        return `还差￥${diff}元起送`
      } else {
        return '去结算'
      }
    },
    payClass () {
      if (this.totalPrice < this.minPrice) {
        return 'not-enough'
      } else {
        return 'enough'
      }
    }
  }
}
</script>
<style>
@import '../../common/css/icon.css';
.shopcart {
    position: fixed;
    left: 0;
    bottom: 0;
    z-index: 50;
    width: 100%;
    height: 48px;
    background: #000;
}
.cart-content {
    display: flex;
    background: #141d27;
}
.content-left {
    flex: 1
}
.content-left .price {
    display: inline-block;
    vertical-align: top;
    margin-top: 12px;
    line-height: 24px;
    padding-right: 12px;
    box-sizing: border-box;
    border-right: 1px solid rgba(255, 255, 255,0.1);
    font-size: 16px;
    color: rgba(255, 255, 255,0.4)
}
.content-left .highlight {
    color: #fff
}
.content-left .deliver {
    display: inline-block;
    vertical-align: top;
    margin: 12px 0 0 12px;
    line-height: 24px;
    font-size: 10px;
    color: rgba(255, 255, 255,0.4)
}
.content-left .logo-wrapper {
    display: inline-block;
    position: relative;
    top: -10px;
    margin: 0 12px;
    padding: 6px;
    width: 56px;
    height: 56px;
    box-sizing: border-box;
    vertical-align: top;
    border-radius: 50%;
    background: #141d27
}
.icon-shopping_cart {
    line-height: 44px;
    color: #80858a;
    font-size: 24px;
}
 .light {
    color: #fff
}
.icon-shopping_cart:before {
  content: "\e907";
}
.content-left .logo {
    width: 100%;
    height: 100%;
    text-align: center;
    margin: 0 auto;
    border-radius: 50%;
    background: #2b343c;
}
.content-left .light {
    background: rgb(0, 160, 220)
}
.logo-wrapper .num {
    position: absolute;
    top: 0;
    right: 0;
    width: 24px;
    height: 16px;
    line-height: 16px;
    text-align: center;
    border-radius: 16px;
    font-size: 9px;
    font-weight: 700;
    color: #fff;
    background: rgb(240, 20, 20);
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.4)
}
.content-right {
    flex: 0 0 105px;
    width: 105px;
}
.pay {
    height: 48px;
    line-height: 48px;
    text-align: center;
    font-size: 12px;
    font-weight: 700;
}
.not-enough {
  background-color: #2b333b;
}
.enough {
  background: #00b43c;
  color: #fff
}
</style>
