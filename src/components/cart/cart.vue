<template>
<div class="shopcart">
    <div class="cart-content">
        <div class="content-left">
            <div class="logo-wrapper">
            <div class="logo">
                <i class="icon-shopping_cart"></i>
            </div>
            <div class="num">{{totalCount}}</div>
        </div>
        <div class="price">￥{{totalPrice}}</div>
        <div class="deliver">另需配送费{{deliveryPrice}}￥</div>
        </div>
        <div class="content-right">
            <div class="pay">￥{{minPrice}}起送</div>
        </div>
    </div>
</div>
</template>
<script>
export default {
  props: {
    selecFoods: {
      type: Array,
      default () {
        return [
          {
            price: 10,
            count: 1
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
      this.selecFoods.forEach(food => {
        total += food.price * food.count
      })
      return total
    },
    totalCount () {
      let count = 0
      this.selecFoods.forEach(food => {
        count += food.count
      })
      return count
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
.icon-shopping_cart:before {
  content: "\e907";
}
.content-left .logo {
    width: 100%;
    width: 100%;
    text-align: center;
    border-radius: 50%;
    background: #2b343c;
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
    background-color: #2b333b;
}
</style>
