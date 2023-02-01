/**
* Created by ztt on 2018/4/19.
*/
<template>
  <div id="">
    <div class="back-bar">
      <div @click="$router.back()" class="back-bar-backBtn">&lt;&nbsp;返回
      </div>
      <div class="back-bar-name">
        销售历史
      </div>
      <div class="back-bar-cancelBtn">
        <router-link to="/sell/sellTable"
                     style="display:block;float:left;width: 25px;height: 25px;font-size: 25px;color: white;font-weight: bolder;">
          <i class="ion-ios-plus-empty"></i>
        </router-link>
        <div
          style="margin-left:8px;display:block;float:left;width: 25px;height: 25px;font-size: 25px;color: white;font-weight: bolder;">
          <i class="ion-ios-search"></i>
        </div>
      </div>
    </div>
    <div class="ok-model-border"></div>
    <div style="margin-top: 56px;">
      <ul style="width: 100%;list-style:none;">
        <li @click="sellTableStatus(0)" :class="{statusActive:isAll}" class="ok-hotsell-time-li">所有</li>
        <li @click="sellTableStatus(1)" :class="{statusActive:isNoPayment}" class="ok-hotsell-time-li">未付款</li>
        <li @click="sellTableStatus(2)" :class="{statusActive:isFinished}" class="ok-hotsell-time-li">有欠款</li>
        <li @click="sellTableStatus(3)" :class="{statusActive:isPaid}" class="ok-hotsell-time-li">已付款</li>
        <li @click="sellTableStatus(4)" :class="{statusActive:isArrearage}" class="ok-hotsell-time-li">已完成</li>
        <li @click="sellTableStatus(5)" :class="{statusActive:isClose}" class="ok-hotsell-time-li">已关闭</li>
        <li @click="sellTableStatus(11)" :class="{statusActive:isNoSend}" class="ok-hotsell-time-li">未发货</li>
        <li @click="sellTableStatus(13)" :class="{statusActive:isReceveied}" class="ok-hotsell-time-li">已送达</li>
      </ul>
    </div>
    <div style="background: #F2F2F2;height: 60px; width: 100%;font-size: 12px;clear: both;line-height: 30px;">
      <i style="color: orange;font-size: 20px;margin-left: 10px;" class="ion-ios-star-outline"></i><span
      style="margin-left: 5px;position:relative;top: -3px;color: #888888">销售单状态&nbsp;&nbsp;:</span>
      <i style="color: #108ee9;font-size: 20px;margin-left: 10px;" class="ion-ios-checkmark-outline"></i><span
      style="margin-left: 5px;position:relative;top: -3px;color: #888888">已付款</span>
      <i style="color: #66CD00;font-size: 20px;margin-left: 10px;" class="ion-ios-checkmark"></i><span
      style="margin-left: 5px;position:relative;top: -3px;color: #888888">已完成</span>
      <i style="color:#575757;font-size: 20px;margin-left: 10px;" class="ion-ios-close-outline"></i><span
      style="margin-left: 5px;position:relative;top: -3px;color: #888888">已关闭</span>
      <div style="margin-left: 105px;">
        <i style="color:#C20C0C;font-size: 20px;margin-left: 10px;" class="ion-clipboard"></i><span
        style="margin-left: 5px;position:relative;top: -3px;color: #888888">有欠款</span>
        <i style="color:orange;font-size: 20px;margin-left: 10px;" class="ion-ios-timer-outline"></i><span
        style="margin-left: 5px;position:relative;top: -3px;color: #888888">未付款</span>
      </div>

    </div>
    <div v-if="orderList.length>0||myData.pageNum==0||loading">
      <van-list
        v-model="loading"
        :finished="finished"
        :offset=100
        @load="onLoad"
      >
        <div v-for="(item,index) in orderList">
          <div class="employee-info-box" style="height: 80px;width: auto;display: block;padding-left: 20px;" @click="soDetails(item)">
            <div style="display: block;float: left;width: 10%;line-height: 80px;font-size: 30px;">

              <i v-if="item.orderStatus==1" style="color:orange" class="ion-ios-timer-outline"></i>
              <i v-if="item.orderStatus==4" style="color:#66CD00" class="ion-ios-checkmark"></i>
              <i v-if="item.orderStatus==3" style="color:#108ee9" class="ion-ios-checkmark-outline"></i>
              <i v-if="item.orderStatus==5" style="color:#575757" class="ion-ios-close-outline"></i>
              <i v-if="item.orderStatus==2" style="color:#C20C0C" class="ion-clipboard"></i>
            </div>
            <div style="display: block;float: left;width: 60%;padding-top: 8px;padding-left: 5px;">
              <div style="display: block;float: left;font-size: 16px;">{{item.customerName}}</div>
              <!-- <div
                style="display: block;float: left;width:auto;color:white;padding-left:3px;padding-right:3px;background: orange;border-radius: 5px;margin-left: 10px;">
                重点客户
              </div> -->
              <div style="clear: both;">{{item.orderNumber}}</div>
              <div>业务时间：{{item.createTime | formateTime('YMDHM')}}</div>
              <div>{{item.remarks}}</div>
            </div>
            <div
              style="font-size:14px;padding-top: 8px;display: block;float: left;width: 30%;text-align: center;">
              <div style="text-decoration: underline;">销：{{item.productCount}}</div>
              <div style="font-size:16px;color: orange;line-height: 40px;">￥{{item.sumPrice | formateMoney}}</div>
              <!--<div style="font-size:12px;color: #888888;">1号仓库</div>-->
            </div>
          </div>
          <div class="ok-model-border"></div>
        </div>
      </van-list>
    </div>
    <div v-if="myData.pageNum!=0&&orderList.length==0&&finished==true" style="color: #888888;text-align: center;padding: 20px;">
      没有此类销售单
    </div>
    <div style="margin-bottom: 56px;"></div>
    <ok-footer></ok-footer>
  </div>
</template>

<script>
  const Footer = resolve => require(['@/components/footer/footer'], resolve);
  import {List} from 'vant';
  import {getSellHistoryList} from '@/service/getData';
  import Vue from 'vue'
  Vue.use(List);
  export default {
    mixins: [],     //混合
    components: {
      'ok-footer':Footer
    },//注册组件
    data() {         //数据
      return {
        isAll: true,
        isNoPayment: false,
        isPaid: false,
        isFinished: false,
        isArrearage: false,
        isClose: false,
        isNoSend: false,
        isReceveied: false,
        orderList:[],
        loading: false,
        finished: false,
        myData:{paging:true,pageNum:0,limit:10,orderStatus:null,orderBy:'create_time desc'}
      };
    },
    computed: {},  //计算属性
    created() {
    },   //创建
    mounted() {
    },   //挂载
    methods: {
      sellTableStatus(n) {
        this.isAll = false;
        this.isNoPayment = false;
        this.isPaid = false;
        this.isFinished = false;
        this.isArrearage = false;
        this.isClose = false;
        this.isNoSend = false;
        this.isReceveied = false;
        switch (n) {
          case 0:
            this.isAll = true;
            this.myData.orderStatus=null;
            this.reLoad();
            break;
          case 1:
            this.isNoPayment = true;
            this.myData.orderStatus=1;
            this.reLoad();
            break;
          case 2:
            this.isFinished = true;
            this.myData.orderStatus=2;
            this.reLoad();
            break;
          case 3:
            this.isPaid = true;
            this.myData.orderStatus=3;
            this.reLoad();
            break;
          case 4:
            this.isArrearage = true;
            this.myData.orderStatus=4;
            this.reLoad();
            break;
          case 5:
            this.isClose = true;
            this.myData.orderStatus=5;
            this.reLoad();
            break;
          case 11:
            this.isNoSend = true;
            this.myData.orderStatus=null;
            this.myData.logisticsStatus=1;
            this.reLoad();
            break;
          case 13:
            this.isReceveied = true;
            this.myData.orderStatus=null;
            this.myData.logisticsStatus=3;
            this.reLoad();
            break;
          default:
            this.isAll = true;
        }
      },
      onLoad() {//上划加载订单历史
        this.myData.pageNum++;
        getSellHistoryList(this.myData).then(
          response => {
              for (var i = 0; i < response.data.results.length; i++) {
                this.orderList.push(response.data.results[i]);
              }
              this.loading = false;
              if (response.data.lastPage) {
                this.finished = true;
              }
          }, error => {
            this.loading = false;
            this.finished = true;
            console.log(error.msg);
          }
        );
      },
      reLoad() {
        this.orderList = [];
        this.myData.pageNum = 0;
        this.finished = false;
        this.onLoad();
      },
      soDetails(item) {
        this.$router.push({path:'/checkstand',query:{saleOrderId:item.id}})
      },
    },   //方法
    watch: {}      //监听
  }
</script>

<style scoped>
  .ok-hotsell-time-li {
    width: 25%;
    height: 30px;
    display: block;
    float: left;
    background: white;
    text-align: center;
    line-height: 30px;
  }

  .statusActive {
    background: #C20C0C !important;
    color: white !important;
  }
</style>
