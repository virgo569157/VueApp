<template>
    <div class="bios-allmain">
        <div class="page-swipe">
            <mt-swipe :auto="2000">
            <mt-swipe-item class="slide1"><img src="../assets/img/bgc1-1.jpg" alt=""></mt-swipe-item>
            <mt-swipe-item class="slide2"><img src="../assets/img/bgc1-2.jpg" alt=""></mt-swipe-item>
            <mt-swipe-item class="slide3"><img src="../assets/img/bgc1-3.jpg" alt=""></mt-swipe-item>
            </mt-swipe>
        </div>
        <div class="bios-main">
            <router-link 
                    v-for="item in oneList"
                    :key="item.id"
                    :to = "{name:'detail',params:{id:item.id}}"
                    tag="div">
            <div class="bios-item">
                <div class="bios-title">{{item.title}}</div>
                <div class="bios-introduce">{{item.description}}</div>
                <div class="item-img"><img :src="item.img" :alt="item.title"></div>
            </div>
            </router-link>
        </div>
    </div>
</template>

<script>
import {mapState,mapMutations} from 'vuex';

export default {
  name: 'one',
  data(){
      return {
          oneList: [],
      }
  },
  mounted(){
    this.getonelList();
  },
  beforeRouteUpdate(to, from , next){
    this.getonelList();
    next();
  },
  beforeRouteEnter(to , from , next){
      next(vm=>{
          vm.changeActive('home')
          vm.changeTitle('首页')
        }
      )
  },
  computed:{
      ...mapState(['isActive'])
  },
  methods:{
      ...mapMutations(['changeActive','changeTitle']),
      getonelList(){
          this.$ajax.getDetailList()
          .then((resp) => {
              this.oneList = resp;
          })
      },
  },
}
</script>

<style lang = 'scss' scoped>

.page-swipe{
    width: 100%;
    height: 200px;
    img{
        width: 100%;
    }
    .slide1{
        width: 100%;
        background: #ccc;
    }
    .slide2{
        width: 100%;
        background: #ccc;
    }
    .slide3{
        width: 100%;
        background: #ccc;
    }
}
.bios-item{
    margin-top: 20px;
    background: #fff;
    position: relative;
    height: 120px;
    width: 100%;
    box-sizing: border-box;
    padding: 10px 10px 10px 120px;
    .item-img{
        position: absolute;
        width: 100px;
        height: 100px;
        background: #acacac;
        top:10px;
        left:10px;
    }
    .bios-title{
        font-size: 18px;
        font-weight: bold;
        color: black;
    }
    .bios-introduce{
        color: #a0a0a0;
        font-size: 15px;
        margin-top: 12px;
        line-height: 24px;
        padding: 18px 0;
        padding-right: 15px;
    }
}
</style>
