<template lang="html">
  <!-- 在首页父组件发送http请求,后将数据通过props传递给子组件,可减少请求次数,减少服务器压力 -->
  <div class="index">
    <v-header/>
    <v-swiper :swiperData="datas.swiper"/>
    <v-service/>
    <v-section1 :list="datas.section1.list" :banner='datas.section1.banner'/>
    <v-section2 :list="datas.section2.list" :banner='datas.section2.banner'/>
    <v-section3/>
    <v-section4 :list="datas.section4.list" :banner='datas.section4.banner'/>
    <v-baseline/>
    <v-footer/>
  </div>
</template>

<script>
import Header from '@/components/index/header.vue'
import Swiper from '@/components/index/swiper.vue'
import Service from '@/components/index/service.vue'
import Section1 from '@/components/index/section1.vue'
import Section2 from '@/components/index/section2.vue'
import Section3 from '@/components/index/section3.vue'
import Section4 from '@/components/index/section4.vue'
import Baseline from '@/common/_baseline.vue'
import Footer from '@/common/_footer.vue'
import index from '@/http/mock.js' //模拟数据
export default {
  components: {
    'v-header': Header,
    'v-swiper': Swiper,
    'v-service': Service,
    'v-section1': Section1,
    'v-section2': Section2,
    'v-section3': Section3,
    'v-section4': Section4,
    'v-baseline': Baseline,
    'v-footer': Footer
  },
  data() {
    return {
      datas: {
        section1:{},
        section2:{},
        section3:{},
        section4:{},
        swiper:[]
      },
      loading: true
    }
  },
 
  beforeCreate() {
     this.$api({
      method: 'post',
      url: '/index'
    }).then((response) => {
      this.datas = response.data;
      this.datas.swiper[0].imgPath="http://106.12.131.109:8083/main/1.jpeg";
      this.datas.swiper[1].imgPath="http://106.12.131.109:8083/main/2.jpeg";
      this.datas.swiper[2].imgPath="http://106.12.131.109:8083/main/3.jpeg";
      this.datas.swiper[3].imgPath="http://106.12.131.109:8083/main/4.jpeg";
    }).catch(function(error) {
      alert(error)
    })
    //this.swiper1[0].id=0;
  }
  
}
</script>



<style lang="less" scoped>
.index {
    width: 100%;
    padding-bottom: 14vw;
    background-color: #F8FCFF;
}
</style>
