<template>
  <div class="cartControl">
    <div class="cart-decrease icon-remove_circle_outline"
         @click="decreaseCart" v-show="food.count>0"></div>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>
</template>

<script>
import Vue from 'vue'
export default {
  name: "cartControl",
  props:{
    food:{
      type:Object
    }
  },
  methods:{
    addCart(){
      if(!this.food.count){
        Vue.set(this.food,'count',1)
      }else {
        this.food.count++;
      }

    },
    decreaseCart(){
      this.food.count--;
    }
  }
}

</script>

<style lang="stylus" ref="stylesheet/stylus">
.cartControl
  .cart-decrease,.cart-add
    display inline-block
    line-height 20px
    font-size 20px
    padding 6px
    color rgb(0,160,220)
  .cart-count
    display inline-block
    vertical-align top
    width 12px
    padding-top 6px
    line-height 24px
    text-align center
    font-size 14px
    color rgb(147,153,159)

</style>
