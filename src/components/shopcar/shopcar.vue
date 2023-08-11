<template>
  <div class="shopCar">
    <div class="content" @click="toggleList">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo" :class="{'highlight':totalCount>0}">
            <span class="icon-shopping_cart" :class="{'highlight':totalCount>0}"></span>
          </div>
          <div v-show="totalCount>0" class="num">{{totalCount}}</div>
        </div>
        <div class="price" :class="{'highlight':totalCount>0}">¥{{totalPrice}}</div>
        <div class="desc">另需配送费¥4</div>
      </div>

      <div class="content-right">
        <div class="pay" :class="payClass">
          {{payDesc}}
        </div>
      </div>
    </div>
    <!--购物车详情    -->
    <transition name="fade">


    <div class="shopCar-list" v-show="listShow">
      <div class="list-header">
        <h1 class="title">购物车</h1>
        <span class="empty">清空</span>
      </div>
      <div class="list-content">
        <ul>
          <li class="food" v-for="food in selectFoods">
            <span class="name">{{food.name}}</span>
            <div class="price">
              <span>¥{{food.price*food.count}}</span>
            </div>
            <div class="cartControl-wrapper">
              <cartControl :food="food"></cartControl>
            </div>
          </li>
        </ul>
      </div>
    </div>
    </transition>
  </div>
</template>

<script>
import CartControl from "../cartcontrol/cartControl.vue";

export default {
  name: "shopcar",
  components: {CartControl},
  props:{
    deliveryPrice:{
      type:Number,
      default:0
    },
    minPrice:{
      type:Number,
      default: 0
    },
    selectFoods:{
      type:Array,
      default(){
        // return[{
        //   price:114514,
        //   count:1
        // }]
      }
    }
  },
  computed:{
    totalPrice(){
      let total = 0;
      this.selectFoods.forEach((food)=>{
        total+=food.price*food.count;
      })
      return total;
    },
    totalCount(){
      let total = 0;
      this.selectFoods.forEach((food)=>{
        total+=food.count;
      })
      return total;
    },
    payDesc(){
      if(this.totalPrice===0){
        return '¥'+this.minPrice+"起送"
      }else if(this.totalPrice < this.minPrice){
        let diff = this.minPrice-this.totalPrice;
        return "还差¥"+diff+"元起送"
      }else{
         return "去结算"
      }
    },
    payClass(){
      if(this.totalPrice<this.minPrice){
        return 'not-enough'
      }else{
        return 'enough'
      }
    },
    listShow(){
      if(!this.totalCount){
        this.fold=true
        return false
      }
      let show=!this.fold
      return show;
    }
  },
  data(){
    return{
      fold:true
    }
  },
  methods:{
    toggleList(){
      if(!this.totalCount){
        return
      }
      this.fold=!this.fold
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
.shopCar
  position fixed
  left 0
  bottom 0
  z-index 50
  width 100%
  height 48px
  background #000
  .content
    display flex
    background #141d27
    .content-left
      flex 1
      .logo-wrapper
        display inline-block
        position relative
        top -10px
        margin 0 12px
        padding 6px
        width 56px
        height 56px
        border-radius 50%
        background #141d27
        .logo
          width 80%
          height 80%
          border-radius 50%
          background #2b343c
          text-align center
          margin-left 5px
          &.highlight
            background rgb(0,160,220)
          .icon-shopping_cart
            line-height 44px
            font-size 24px
            color #80858a
            &.highlight
              color #fff
        .num
          position: absolute;
          top 0
          right 0
          width 24px
          height 16px
          line-height 16px
          text-align center
          border-radius 16px
          font-size 9px
          font-weight 700
          color #fff
          background rgb(240,20,20)
      .price
        display inline-block
        vertical-align top
        margin-top 12px
        line-height 24px
        padding-right 12px
        border-right 1px solid rgba(255,255,255,0.4)
        font-size 16px
        font-weight 700
        color rgba(255,255,255,0.4)
        &.highlight
          color #fff
      .desc
        display inline-block
        vertical-align top
        margin 12px 0 0 12px
        line-height 24px
        color rgba(255,255,255,0.4)
        font-size 10px
    .content-right
      flex 0 0 105px
      width 105px
      .pay
        height 48px
        line-height 48px
        font-size 12px
        text-align center
        color rgba(255,255,255,0.4)
        font-weight 700
        background #2b333b
        &.not-enough
          background #2b333b
        &.enough
          background #00b43c
          color #fff
  .shopCar-list
    position absolute
    left 0
    top 0
    z-index -1
    width 100%
    height 220px
    transform  translate3d(0,-100%,0)//整个列表相对于自身的高度偏移
    &.fade-enter-active,&.fade-leave-active
      transition all 0.5s linear
      transform translate3d(0,-100%,0)
    &.fade-enter,&.fade-leave-active
      transform translate3d(0,0,0)
    .list-header
      height 40px
      line-height 40px
      padding 0 18px
      background #f3f5f7
      border-bottom 1px solid rgba(7,17,27,0.1)
      .title
        float left
        font-size 14px
        color rgb(7,17,27)
      .empty
        float right
        font-size 12px
        color rgb(0,160,220)
    .list-content
      padding 0 18px
      max-height 200px
      background #fff
      overflow hidden
      .food
        .name,.price,.cartControl-wrapper
          display inline-block



</style>
