<template>
    <div class="cartcontrol">
      <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0"></div>
      <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
      <div class="cart-add icon-add_circle"></div>
    </div>
</template>
<script>
export default {
  props: {
    food: {
      type: Object
    }
  },
  created () {
    console.log(this.food)
  }
}
</script>
<style>
@import '../../common/css/icon.css';
.cartcontrol {
  font-size: 0;
}
.cartcontrol .cart-decrease {
  display: inline-block;
  padding: 6px;
  line-height: 24px;
  font-size: 24px;
  color: rgb(0, 160, 220)
}
.cartcontrol .cart-count {
  display: inline-block
}
.cartcontrol .cart-add {
  display: inline-block;
  line-height: 24px;
  font-size: 24px;
  color: rgb(0, 160, 220)
}
</style>
