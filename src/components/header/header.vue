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
          <span class="icon"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
    </div>
    <!--公告-->
    <div class="bulletin-wrapper"></div>
  </div>
</template>

<script>
export default {
  name: "header",
  props:{
    seller:{
      type:Object
    }
  }

}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import "../../common/stylus/mixin.styl"
.header
  color #fff
  background #000
  .content-wrapper
    padding 24px 12px 18px 24px
    .avatar
      display inline-block
      vertical-align top
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

</style>
