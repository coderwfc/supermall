<template>
  <div class="wrapper" ref="wrapper">
    <div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
export default {
  name: "Scroll",
  data(){
    return {
      scroll:null
    }
  },
  props:{
    probeType:{
      type:Number,
      default:0
    },
    pullUpLoad:{
      type:Boolean,
      default: false
    }
  },
  mounted() {
    this.scroll = new BScroll(this.$refs.wrapper,{
      click:true,
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad
    })
    this.scroll.on('scroll',(position)=>{
      this.$emit('hideOr',position)
    })
    this.scroll.on('pullingUp',()=>{
      this.$emit('pullUpLoad')
    })
  },
  methods:{
    scrollTo(x,y,time=500){
     this.scroll && this.scroll.scrollTo(x,y,time)
    },
    refresh(){
      // console.log('...');
      this.scroll &&  this.scroll.refresh()
    },
    getsaveY(){
      return  this.scroll ? this.scroll.y : 0
    }
  }
}
</script>

<style scoped>

</style>