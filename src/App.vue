<template>
  <div class="app-container">
    <Header></Header>
    <!-- 循环渲染goods里面的信息 -->
    <Goods v-for="item in list" :key="item.id" :title="item.goods_name" :pic="item.goods_img" 
    :price="item.goods_price" :status="item.goods_state"></Goods>
    <h1>App 根组件</h1>
  </div>
</template>

<script>
//导入axios请求库
import axios from 'axios'
import Header from './components/Header/Header.vue'
import Goods from './components/Goods/Goods.vue'
export default {
  components:{
    Header,
    Goods,
  },
  data(){
    return {
      list:[],
    }
  },
  methods:{
    //封装请求列表数据的方法
    async initCartList(){
      const {data:res} = await axios.get('https://www.escook.cn/api/cart')
      //只要请求回来的数据，在页面渲染期间要用到，则必须转存到data中
      if(res.status === 200){
        this.list = res.list
      }
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
