<template>
  <div id="app">
    <mt-button type="default" size="small" @click="btnAction">default</mt-button>
    <mt-button type="primary" size="large" @click="btnAction2">primary</mt-button>
    <mt-button type="danger" size="normal" @click="btnAction3" plain>danger</mt-button>
    <router-view/>

    <mt-loadmore :top-method="loadTop" :bottom-method="loadBottom" :bottom-all-loaded="allLoaded" ref="loadmore">
      <ul v-infinite-scroll ="loadMore" infinite-scroll-disabled="loading" infinite-scroll-distance="50">
        <li v-for="(item,index) in list" :key="index">{{ item }}</li>
      </ul>
    </mt-loadmore>


    <mt-actionsheet
    :actions="actions"
    v-model="sheetVisible">
  </mt-actionsheet>

  
  </div>
</template>

<script>
import Vue from "vue"
import {Button} from "mint-ui"
import { Toast,Indicator,Loadmore,InfiniteScroll,MessageBox,Actionsheet } from 'mint-ui'
Vue.component(Button.name,Button)
Vue.component(Loadmore.name,Loadmore)
Vue.component(Actionsheet.name,Actionsheet)
Vue.use(InfiniteScroll)

export default {
  name: 'App',
  data(){
    return {
      list:[1,2,3,4],
      loading:false,
      actions:[{name:"拍照"},{name:"从相册中选取"}],
      sheetVisible:false
    }
  },
  methods:{
    btnAction(){
      Toast("hello wordl");
      Indicator.open("加载中···")
    },
    btnAction2(){
      MessageBox({
        title: '提示',
        message: '确定执行此操作?',
        showCancelButton: true
      });
    },
    btnAction3(){
      this.sheetVisible = true;
    },
    loadTop(){
      // this.$refs.loadmore.onTopLoaded();
    },
    loadMore(){
      this.loading = true;
      setTimeout(() => {
        let last = this.list[this.list.length - 1];
        for (let i = 1; i <= 10; i++) {
          this.list.push(last + i);
        }
        this.loading = false;
      }, 2500);
    }

  }
}
</script>

<style>
li{
  height: 100px;;
}
</style>
