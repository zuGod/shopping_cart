<template>
  <div class="app-container">
    <Header></Header>
    <!-- 循环渲染goods里面的信息 -->
    <Goods v-for="item in list" :key="item.id" :id="item.id" :title="item.goods_name" :pic="item.goods_img" 
    :price="item.goods_price" :status="item.goods_state" :count="item.goods_count"
      @count-change="getNewState"></Goods>
      <Footer :fullState="fullState" @checked-change="getNewChecked" :amt="amt" :countNum="countNum"></Footer>
  </div>
</template>

<script>
//导入axios请求库
import axios from 'axios'
import Header from './components/Header/Header.vue'
import Goods from './components/Goods/Goods.vue'
import Footer from './components/Footer/Footer.vue'
import bus from './components/eventBus'
export default {
  components:{
    Header,
    Goods,
    Footer,
  },
  data(){
    return {
      list:[],
    }
  },
  computed:{
    //动态计算全选的状态是true韩式false
    fullState(){
      return this.list.every(item => item.goods_state)
    },
    amt(){
      //1.先过滤
      //2.再reduce累加
      return this.list.filter(item => item.goods_state).reduce((total,item) => {
        return total += item.goods_price * item.goods_count
      },0)
    },
    countNum(){
      return this.list.filter(item => item.goods_state).reduce((num,item) => {
        return num += item.goods_count
      },0)
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
    //e的格式为{id,value}
    getNewState(e){
      console.log(1)
      this.list.some(item =>{
        if(item.id === e.id){
          item.goods_state = e.value
          //终止后续的循环
          return true
        }
      })
    },
    getNewChecked(e){
      this.list.forEach((item) => {
        item.goods_state = e.value
      })
    },
  },
  created(){
    this.initCartList();

    bus.$on('share',val => {
      this.list.some(item => {
        if(item.id === val.id){
          item.goods_count = val.value
        }
      })
    });

    bus.$on('subtract',val =>{
      this.list.some(item =>{
        if(item.id === val.id && val.value >= 0){
          item.goods_count = val.value
        }
      })
    })
  }
}
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
