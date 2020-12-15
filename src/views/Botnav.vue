<template>
    <div>
        <transition :name="transitionName">
            <router-view class="Router"></router-view>
        </transition>
        <cube-tab-bar
            v-model="selectedLabelDefault"
            :data="tabs"
            @click="clickHandler"
            @change="changeHandler"
            class="botnav"
            >
        </cube-tab-bar>
        <span class="countsum">{{ countsum }}</span>
    </div>
    
</template>
<script>
import {mapGetters} from 'vuex'
export default {
  data () {
    return {
      transitionName:'slide-fade',//这里进行一个动画自左向右或者自右向左的一个动画效果
      selectedLabelDefault: '首页',
      tabs: [{
        label: '首页',
        icon: 'cubeic-home'
      }, {
        label: '分类',
        icon: 'cubeic-more'
      }, {
        label: '搜索',
        icon: 'cubeic-search'
      }, {
        label: '购物车',
        icon: 'cubeic-mall'
      },
      {
        label: '我的',
        icon: 'cubeic-person'
      }
      ]
    }
  },
  methods: {
    clickHandler (label) {
      // if you clicked home tab, then print 'Home'
      // console.log(label)
    },
    changeHandler (label) {
      // if you clicked different tab, this methods can be emitted
      //这里是点击与自身不同的其他导航进行跳转到新的路由页面
      switch (label) {
        case '首页':
        this.$router.push('/botnav/index');
        break;
        case '分类':
        this.$router.push({path:'/botnav/list'});
        break;
        case '搜索':
        this.$router.push({path:'/botnav/search'});
        case '购物车' :
        this.$router.push({path:'/botnav/cart'});
        break;
        case '我的' :
        this.$router.push({path:'/botnav/mine'});
        break;
      }
    }
  },
  computed:{
    ...mapGetters({
      countsum : 'countsum'
    })
  },
  created(){
    switch(this.$route.path){
      case '/botnav/index':
      this.selectedLabelDefault = '首页';
      break;
      case '/botnav/list':
      this.selectedLabelDefault = '分类';
      break;
      case '/botnav/search':
      this.selectedLabelDefault = '搜索';
      break;
      case '/botnav/cart':
      this.selectedLabelDefault = '购物车';
      break;
      case '/botnav/mine':
      this.selectedLabelDefault = '我的';
      break;
    }
  }

}
</script>
<style lang="stylus" >
    .cube-tab-bar.botnav
        position  fixed 
        bottom  0
        left 0
        z-index 1000
        width 100%
        background #ffffff
        .cube-tab div
            font-size 16px
            padding-top 3px
        i 
            font-size 20px
        
        .slide-fade-enter-active 
            transition  all .3s ease;
        
          .slide-fade-leave-active 
            transition all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
          
          .slide-fade-enter, .slide-fade-leave-to
         
            transform translateX(10px);
            opacity 0;

  .countsum
      position  fixed
      bottom 33px
      right 23%
      z-index  1001
      width 18px
      height 18px
      line-height 18px
      border-radius 50%
      font-size 14px
      background red
      color #fff
  
</style>