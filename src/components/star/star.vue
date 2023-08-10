<template>
  <div class="start">
    <span v-for="itemClass in itemClasses" :class="itemClass" class="star-item"></span>
  </div>
</template>

<script>

const LENGTH = 5
const CLS_ON='on';const CLS_HALF='half';const CLS_OFF='off';
export default {
  name: "star",
  props:{
    score:{
      type:Number
    }
  },
  computed:{
    itemClasses(){
      let result=[]
      let score = Math.floor(this.score*2)/2
      //判断是否有半心
      let hasDecimal = score%1!==0
      let integer = Math.floor(score)
      //先放全心
      for(let i = 0;i < integer; i++){
        result.push(CLS_ON)
      }
      if(hasDecimal){
        result.push(CLS_HALF)
      }
      while(result.length<LENGTH){
        result.push(CLS_OFF)
      }
      return result
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import "../../common/stylus/mixin.styl"
.start
  .star-item
    display inline-block
    width 20px
    height 20px
    margin-right 22px
    background-size 20px 20px
    &.on
      bg-image('star24_on')
    &.off
      bg-image('star24_off')
    &.half
      bg-image('star24_half')

</style>
