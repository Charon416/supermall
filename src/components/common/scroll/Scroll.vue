<template>
<!-- ref绑定给自组件 -->
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
  
</template>

<script>
  import BScroll from 'better-scroll'
  export default {
    name:'Scroll',
    props:{
      probeType:{
        type: Number,
        default: 0
      },
      pullUpLoad:{
        type:Boolean,
        default:true
      }
      
    },
    data(){
      return {
        scroll:null,
 
      }

    },
    mounted(){
      // 1,创建对象
      this.scroll=new BScroll(this.$refs.wrapper,{
        click:true,
        probeType:this.probeType,
        pullUpLoad:this.pullUpLoad
      })
      // 2,监听滚动的位置
      if(this.probeType == 2 || this.probeType == 3){
        this.scroll.on('scroll',(position) => {
        this.$emit('scroll',position)
      })
      }


      // 3，监听scroll滚动到底部事件
      if(this.pullUpLoad){
        this.scroll.on('pullingUp',() => {
        this.$emit('pullingUp')
      })
      }

      //监听scroll滚动到底部
      if(this.pullUpLoad){

      }





    },
    methods:{
      scrollTo(x,y,time=300){
        this.scroll && this.scroll.scrollTo(x,y,time)
      },
      // 完成加载更多
      finishPullUp(){
        
        this.scroll && this.scroll.finishPullUp()
      },

      refresh(){
        // console.log('-----');
        this.scroll && this.scroll.refresh()

      },
      getScrollY(){
        return this.scroll ? this.scroll.y : 0
      }
    }

  }
</script >

<style scoped>

</style>