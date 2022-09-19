<template>
  <div class="app-container">
    <Header></Header>
    <h1>App 根组件</h1>
  </div>
</template>

<script>
//导入axios请求库
import axios from 'axios'
import Header from './components/Header/Header.vue'
export default {
  components:{
    Header,
  },
  methods:{
    //封装请求列表数据的方法
    async initCartList(){
      const {data:res} = await axios.get('https://www.escook.cn/api/cart')
      console.log(res)
    },
  },
  created(){
    this.initCartList()
  }
}
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
