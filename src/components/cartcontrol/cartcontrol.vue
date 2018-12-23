<template>
    <div class="cartcontrol">
      <div class="cart-decrease icon-remove_circle_outline" @click="decreaseCart" v-show="food.count>0"></div>
      <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
      <div class="cart-add icon-add_circle" @click="addCart"></div>
    </div>
</template>
<script>
import Vue from 'vue'
export default {
  props: {
    food: {
      type: Object
    }
  },
  created () {
    // console.log(this.food)
  },
  methods: {
    addCart (event) {
      if (!event._constructed) {
        return
      }
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1)
      } else {
        this.food.count++
      }
    },
    decreaseCart () {
      if (!event._constructed) {
        return
      }
      if (this.food.count) {
        this.food.count--
      }
    }
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
  /* padding: 6px; */
  line-height: 24px;
  font-size: 24px;
  color: rgb(0, 160, 220)
}
.cart-count {
  display: inline-block;
  /* vertical-align: top; */
  width: 12px;
  padding: 0 6px 0 6px;
  line-height: 24px;
  text-align: center;
  font-size: 24px;
  color: rgb(147, 153, 159)
}
.cartcontrol .cart-add {
  display: inline-block;
  line-height: 24px;
  font-size: 24px;
  color: rgb(0, 160, 220)
}
</style>
