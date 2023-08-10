<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <!--头像-->
        <img :src="seller.avatar" width="64" height="64">
      </div>
      <!--内容 分三块-->
      <div class="content">
        <div class="title">
          <!--品牌-->
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <!--描述-->
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <!--优惠-->
        <div class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <!--5个-->
      <div class="support-count">
        <span class="count">{{seller.supports.length+"个"}}</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <!--公告-->
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <!--头部背景-->
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
<!--详情    -->
    <div v-show="detailShow" class="detail">
      <div class="detail-wrapper">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
          <div class="star-wrapper">
            <star :score="seller.score"></star>
          </div>
        </div>

        <div class="detail-disCountDetails">
          <!--标题-->
          <div class="disCountDetails-title">
            <div class="Line"></div>
            <div class="details-main">优惠信息</div>
            <div class="Line"></div>
          </div>
          <!--内容          -->
          <div class="disCountDetails-main">
            <div class="item" v-for="item in seller.supports">
              <span class="icon" :class="classMap[item.type]"></span>
              <span class="text">{{item.description}}</span>
            </div>
          </div>
          <!--公告          -->
          <div class="bulletin">
            <div class="bulletin-title">
              <div class="Line"></div>
              <div class="details-main">商家公告</div>
              <div class="Line"></div>
            </div>
            <div class="bulletin-text">
              <span class="text">{{seller.bulletin}}</span>
            </div>

          </div>
        </div>
      </div>
      <div class="detail-close">
        <i class="icon-close"></i>
      </div>
    </div>


  </div>

</template>

<script>
import star from "../star/star.vue"
export default {
  name: "header",
  props:{
    seller:{
      type:Object
    }
  },
  created() {
    this.classMap=['decrease','discount','special','invoice','guarantee']
  },
  data(){
    return{
      detailShow:true
    }
  },
  components:{star}

}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import "../../common/stylus/mixin.styl"
.header
  color #fff
  background rgba(7,17,27,0.25)
  position relative
  .content-wrapper
    padding 24px 12px 18px 24px
    position: relative;
    .avatar
      display inline-block
      vertical-align top
      img
        border-radius 5px
    .content
      display inline-block
      margin-left 16px
      font-size 14px
      .title
        margin 2px 0 8px 0
        .brand
          display inline-block
          width 30px
          height 18px
          bg-image('brand')
          background-size 30px 18px
          vertical-align top
        .name
          margin-left 6px
          font-size 16px
          line-height 18px
          font-weight bolder
      .description
        margin-bottom 10px
        line-height 12px
        font-size 12px
      .support
        .icon
          display inline-block
          width 12px
          height 12px
          margin-right 4px
          background-size 12px 12px
          &.decrease
            bg-image('decrease_1')
          &.discount
            bg-image('discount_1')
          &.special
            bg-image('special_1')
          &.invoice
            bg-image('invoice_1')
          &.guarantee
            bg-image('guarantee_1')
        .text
          line-height 12px
          font-size 12px


    .support-count
      position absolute
      bottom 15px
      right 12px
      padding 0 8px
      height 24px
      line-height 24px
      border-radius 14px
      background rgba(0,0,0,0.2)
      text-align center
      .count
        vertical-align top
        font-size 10px
      .icon-keyboard_arrow_right
        margin-left 2px
        line-height 24px
        font-size 10px
  .bulletin-wrapper
    height 28px
    line-height 28px
    padding 0 22px 0 12px
    white-space nowrap //强制同一行超出的文本不换行
    overflow hidden
    text-overflow ellipsis //多出去的用。。。表示
    position: relative;
    background rgba(7,17,27,0.2)
    .bulletin-title
      display inline-block
      vertical-align top
      margin-top 7px
      width 22px
      height 12px
      bg-image('bulletin')
      background-size 22px 12px

    .bulletin-text
      vertical-align top
      margin 0 4px
      font-size 10px
    .icon-keyboard_arrow_right
      position: absolute;
      font-size 10px
      right 12px
      top 8px
  .background
    position: absolute;
    top 0
    left 0
    width 100%
    height 100%
    z-index -1
    filter blur(10px)
  .detail
    position: fixed;
    z-index 100
    top 0
    left 0
    overflow hidden
    width 100%
    height 100%
    background rgba(7,17,27,0.8)
    .detail-wrapper
      .detail-main
        margin-top 64px
        padding-bottom 24px
        .name
          line-height 16px
          text-align center
          font-size 16px
          font-weight 700
        .star-wrapper
          margin-left 18px
          padding 2px
          text-align center
          margin-top 30px
      .detail-disCountDetails
        //background-color wheat
        padding-left 36px
        padding-right 36px
        //height 15px
        .disCountDetails-title
          text-align center
          .Line
            background-color rgba(255,255,255,0.2)
            height 1px
            width 32%
            display inline-block

            position relative
            margin-bottom 7px
          .details-main
            font-size 18px
            display inline-block
            padding  0 12px 0 12px
            font-weight 800


        .disCountDetails-main
          margin-top 24px
          .item
            margin-bottom 12px
            margin-left 12px
            .icon
              display inline-block
              width 16px
              height 16px
              margin-right 6px
              background-size 16px 16px
              &.decrease
                bg-image('decrease_1')
              &.discount
                bg-image('discount_1')
              &.special
                bg-image('special_1')
              &.invoice
                bg-image('invoice_1')
              &.guarantee
                bg-image('guarantee_1')
            .text
              line-height 16px
              font-size 16px
              font-weight 200
        .bulletin
          margin-top 32px
          .bulletin-title
            text-align center
            .Line
              background-color rgba(255,255,255,0.2)
              height 1px
              width 32%
              display inline-block
              position relative
              margin-bottom 7px
            .details-main
              font-size 18px
              font-weight 800
              display inline-block
              padding  0 12px 0 12px
          .bulletin-text
            margin 24px 12px auto 24px
            .text
              font-size 16px
              font-weight 200
              color rgb(255,255,255)
              line-height 25px
    .detail-close
        position: absolute;
        bottom 32px
        width 32px
        height 32px
        margin-left 50%
        left -16px
        font-size 32px
</style>
