<template>
  <div class="tabControl">
    <div v-for="(item,index) in title"
         class="tabControl-item" :class="{active:currentIndex === index}"
         @click="itemClick(index)">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabControl",
  props:{
    title:{
      type:Array,
      default(){
        return []
      }
    }
  },
  data(){
    return {
      currentIndex:0
    }
  },
  methods:{
    itemClick(index){
      this.currentIndex = index
      this.$emit('tabClick',index)
    }
  }
}
</script>

<style scoped>
  .tabControl {
    display: flex;
    text-align: center;
    margin-top: 10px;
    background-color: #ffffff;
  }
  .tabControl-item {
    flex: 1;
    font-size: 15px;
    height: 40px;
    line-height: 40px;
    width: 100%;
  }
  .active {
    color: var(--color-high-text);
  }
  .active span {
    padding: 3px;
    border-bottom: 3px solid var(--color-tint);
  }

</style>