<template>
  <div class="number-container d-flex justify-content-center align-items-center">
    <!-- 减 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="sub">-</button>
    <!-- 购买的数量 -->
    <span class="number-box">{{ num }}</span>
    <!-- 加 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="add">+</button>
  </div>
</template>

<script>
import bus from '../eventBus'
export default {
  //props只读
  props:{
    num:{
      type:Number,
      default:'1'
    },
    id:{
      type: Number,
      require:true
    }
  },
  methods:{
    add(){
      var obj = {
        id:this.id,
        value: this.num + 1
      }
      bus.$emit('share',obj)
    },
    sub(){
      var obj = {
        id:this.id,
        
        value:this.num - 1
      }
      bus.$emit('subtract',obj)
    },
  }
}
</script>

<style lang="less" scoped>
.number-box {
  min-width: 30px;
  text-align: center;
  margin: 0 5px;
  font-size: 12px;
}

.btn-sm {
  width: 30px;
}
</style>
