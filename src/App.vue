<template>
  <div id="app">
    <div class="header">
      <v-header :seller="seller"></v-header>
    </div>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link></div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link></div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link></div>
    </div>
    <router-view :seller="seller"/>
    <div class="content">
    </div>

  </div>
</template>

<script>
import header from "./components/header/header.vue"
export default {
  name: 'App',
  components:{
    'v-header':header
  },
  data(){
    return{
      seller:{}
    }
  },
  created() {
    this.$http.get('/api/seller').then((response)=>{
      // console.log(response)
      response=response.body;
      if(response.errno===0){
        this.seller=response.data;
        console.log(this.seller)
      }
    });
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
/*  #app .tab{
    display: flex;!*类似float*!
    width: 100%;
    height: 40px;
    line-height: 40px;
  }
  #app .tab .tab-item{
    flex: 1;
    text-align: center;
  }
  #app .tab .tab-item a{
    display: block;
    font-size: 14px;
    color: rgb(77,85,93);
  }
  #app .tab .tab-item a:hover{
    color: rgb(240,20,20);
  }*/
@import "./common/stylus/mixin.styl"
  #app
    .tab
      display flex
      width 100%
      height 40px
      line-height 40px
      //border-bottom 1px solid rgba(7,17,27,0,1)
      border-1px(rgba(7,17,27,0,1))
      .tab-item
        flex 1
        text-align center
        & > a
          display block
          font-size 14px
          color rgb(77,85,93)
        & .router-link-active
          color rgb(240,20,20)
</style>
