/**
* Created by ztt on 2018/5/12.
*收银台
*/
<template>
    <div id="">
      <div>
        <div style="color: white;height:56px;background:#C20C0C;font-size: 18px;margin: 0 auto;width: 100%;text-align: center;line-height: 56px;">
          <span>销售单详情</span>
          <span @click="$router.back()" style="float: left;font-size: 25px;width: 56px;height: 20px;color: white;margin-left: 10px;" >
            <i class="ion-ios-arrow-left"></i><span style="font-size: 16px;position:relative;top: -3px;">&nbsp;返回</span>
          </span>
          <div style="float: right;font-size: 25px;width: 56px;height: 20px;" >
            <i></i>
          </div>
        </div>
        <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
          <div style="width:25%;display: block;float: left;padding-left: 20px;">销售单号</div>
          <div style="height:43px;width:70%;display: block;float: left;">
            <input style="height: 30px;font-size: 14px;width: 100%;padding-left: 30px" disabled placeholder="请输入订单号" type="text" v-model="orderNumber"/>
          </div>
        </div>
        <div class="ok-model-border"></div>
        <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
          <div style="width:25%;display: block;float: left;padding-left: 20px;">客户名称</div>
          <div style="height:43px;width:70%;display: block;float: left;">
            <input style="height: 30px;font-size: 14px;width: 100%;padding-left: 30px" disabled placeholder="零售客户" type="text" v-model="customerName"/>
          </div>
        </div>
        <div class="ok-model-border"></div>
        <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
          <div style="width:25%;display: block;float: left;padding-left: 20px;">备注</div>
          <div style="height:43px;width:70%;display: block;float: left;">
            <input style="height: 30px;font-size: 14px;width: 100%;padding-left: 30px" disabled type="text" v-model="remarks"/>
          </div>
        </div>
        <!-- <div class="ok-model-border"></div>
        <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
          <div style="width:25%;display: block;float: left;padding-left: 20px;">商品数量</div>
          <div style="height:43px;width:70%;display: block;float: left;">
            <input style="height: 30px;font-size: 16px;width: 100%;padding-left: 30px" disabled placeholder="0" type="number"/>
          </div>
        </div> -->
        <!-- <div class="ok-border"></div>
        <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
          <div style="width:25%;display: block;float: left;padding-left: 20px;font-size: 12px;">整单折扣(%)</div>
          <div style="height:43px;width:70%;display: block;float: left;">
            <input style="height: 30px;font-size: 16px;width: 100%;padding-left: 30px"  placeholder="100" v-model="discount" type="number"/>
          </div>
        </div> -->
        <div class="ok-model-border"></div>
        <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
          <div style="width:25%;display: block;float: left;padding-left: 20px;">应收金额</div>
          <div style="height:43px;width:70%;display: block;float: left;">
            <input style="height: 30px;font-size: 16px;width: 100%;padding-left: 30px" disabled type="number" v-model="sumPrice"/>
          </div>
        </div>
        <div class="ok-model-border"></div>
        <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
          <div style="width:25%;display: block;float: left;padding-left: 20px;">已付金额</div>
          <div style="height:43px;width:70%;display: block;float: left;">
            <input style="height: 30px;font-size: 16px;width: 100%;padding-left: 30px" disabled type="number" v-model="realPay"/>
          </div>
        </div>
        <div class="ok-model-border"></div>
        <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
          <div style="width:25%;display: block;float: left;padding-left: 20px;">未付金额</div>
          <div style="height:43px;width:40%;display: block;float: left;">
            <input style="height: 30px;font-size: 16px;width: 100%;color: orange;padding-left: 30px" disabled type="number" v-model="paymoney"/>
          </div>
          <!-- <div style="height:20px;margin-top:10px;width:10%;display: block;float: left;font-size: 12px;background: orange;text-align: center;border-radius: 3px;color: white;line-height: 20px;">抹零</div>
          <div style="height:43px;width:20%;display: block;float: left;">
            <input style="height: 30px;font-size: 12px;width: 100%;padding-left: 10px;" placeholder="0.00" type="number" v-model="notSmallChange"/>
          </div> -->
        </div>
        
        <div class="ok-border"></div>
        <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
          <div style="width:25%;display: block;float: left;padding-left: 20px;">结算方式</div>
          <div style="height:43px;width:70%;display: block;float: left;">
            <input style="height: 30px;font-size: 14px;width: 100%;padding-left: 30px;color: black;" disabled placeholder="现金" type="text" v-model="payType"/>
          </div>
        </div>
        <div class="ok-model-border"></div>
        <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
          <div style="width:33%;display: block;float: left;padding-left: 20px;">收款金额</div>
          <div style="height:37px;width:40%;display: block;float: left;border-bottom: 1px solid #2D84FF;">
            <input style="height: 30px;font-size: 14px;width: 100%;color: black;" placeholder="0.00" type="number" v-model="parentData.pay1Money" />
          </div>

          <div @click="computPay1Money" style="height:20px;margin-top:10px;width:10%;display: block;float: right;font-size: 12px;background: white;text-align: center;border-radius: 3px;color: #108ee9;line-height: 20px;border: 1px solid #108ee9;margin-right: 15px;">
            全款
          </div>
        </div>
        <div style="margin-top: 5px;" class="ok-model-border"></div>
        <div v-if="showUnit">
          <div class="ok-border"></div>
          <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
            <div style="width:25%;display: block;float: left;padding-left: 20px;">结算方式2</div>
            <div style="height:43px;width:70%;display: block;float: left;">
              <input style="height: 30px;font-size: 14px;width: 100%;padding-left: 30px;color: black;" disabled placeholder="支付宝" type="text" v-model="payType2"/>
            </div>
          </div>
          <div class="ok-model-border"></div>
          <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
            <div style="width:33%;display: block;float: left;padding-left: 20px;">收款金额</div>
            <div style="height:37px;width:40%;display: block;float: left;border-bottom: 1px solid #2D84FF;">
              <input style="height: 30px;font-size: 14px;width: 100%;color: black;" placeholder="0.00" type="number" v-model="parentData.pay2Money"/>
            </div>
            <div @click="computPay2Money" style="height:20px;margin-top:10px;width:10%;display: block;float: right;font-size: 12px;background: white;text-align: center;border-radius: 3px;color: #108ee9;line-height: 20px;border: 1px solid #108ee9;margin-right: 15px;">补款</div>
          </div>
          <div style="margin-top: 5px;" class="ok-model-border"></div>
          <div style="margin:10px;float:right;background: white;padding-left: 10px;padding-right: 10px;width: auto;height: 20px;line-height:20px;color: black;font-size: 10px;">收款合计：￥{{totalMoney | formateMoney}}</div>
        </div>
        <div style="clear: both;" class="ok-model-border"></div>
        <!-- <div @click="showUnitPay" :class="[showUnit?'showunit':'']" style="margin:10px;float:right;background: #108ee9;padding-left: 10px;padding-right: 10px;width: auto;height: 20px;line-height:20px;color: white;font-size: 10px;">{{showUnit?'取消组合':'组合收款'}}</div> -->
        <div style="clear: both;" class="ok-border"></div>
        <!--<div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">-->
          <!--<div style="width:25%;display: block;float: left;padding-left: 20px;">欠款</div>-->
          <!--<div style="height:43px;width:40%;display: block;float: right;border-bottom: 1px solid #2D84FF;margin-right: 15px;">-->
            <!--<input style="height: 30px;font-size: 14px;width: 100%;color: black;" type="number" v-model="debtMony"/>-->
          <!--</div>-->
        <!--</div>-->
        <div class="ok-model-border"></div>
          <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
            <div style="width:33%;display: block;float: left;padding-left: 20px;">欠款金额</div>
            <div style="height:37px;width:40%;display: block;float: left;border-bottom: 1px solid #2D84FF;">
              <input style="height: 30px;font-size: 14px;width: 100%;color: black;" placeholder="0.00" disabled type="number" v-model="debtMony" />
            </div>
          </div>
        <!-- <div style="width: 100%;height: 40px;line-height: 40px;font-size: 16px;color: #888888">
          <div style="width:25%;display: block;float: left;padding-left: 20px;">备注</div>
          <div style="height:43px;width:70%;display: block;float: left;border-bottom: 1px solid #2D84FF;">
            <input style="height: 30px;font-size: 14px;width: 100%;color: black;" type="text" v-model="remark"/>
          </div>
        </div> -->
        <div class="ok-model-border"></div>
        <div style="width: 100%;">
          <div v-for="item in item.saleOrderItemVos" class="ok-text-box" style="width: 100%; margin: 0 0 10px 0; height: 50px; display: auto;">
            <div class="ok-text-name" style="width: auto;">商品名称：<span style="color: #C20C0C;" class="ok-product-details-name">{{item.productName}}</span></div><br>
            <div class="ok-text-name2" style="margin-left: 1%;width: 100%">
              商品数量：<span style="color: #C20C0C">{{item.saleCount}}</span>   <span style="margin-left: 3%">销售价：<span style="color: #C20C0C">{{item.salePrice}}</span></span>
            </div>
          </div>
          
        </div>
        <div style="margin-top: 15px;" class="ok-border"></div>
      </div>
      <div style="position: fixed;bottom: 0px; width: 100%;">
        <div v-if="item.orderStatus==1 || item.orderStatus==2" @click="toGatheringPage" style="height: 40px;width: 100%;background: #5cb85c; color: white;text-align: center;line-height: 40px; margin-bottom: 5px;">去结账</div>
        <div v-if="item.logisticsStatus!=3 && item.orderStatus!=5" @click="confirmReceipt" style="height: 40px;width: 100%;background: #337ab7; color: white;text-align: center;line-height: 40px; margin-bottom: 5px;">确认收货</div>
        <div v-if="item.orderStatus==1" @click="closeOrder" style="height: 40px;width: 100%;background: #c9302c; color: white;text-align: center;line-height: 40px; margin-bottom: 5px;">关闭订单</div>
      </div>
      
      <!-- <ok-gathering
        :parentData="parentData"
      ></ok-gathering> -->
    </div>
</template>

<script>
  import Gathering from '@/pages/checkstand/gathering'
  import {pay, getSellOrderById, closeSoById, confirmReceiptById} from '@/service/getData.js'
  import { Toast } from 'vant';
    export default {
        mixins: [],     //混合
        components: {
          'ok-gathering':Gathering
        },//注册组件
        data() {         //数据
            return {
              item: {
                saleOrderItemVos: []
              },
              sumPrice: 0.00,
              realPay: 0.00,
              toBePaid: 0.00,
              paymoney:0.00,//应付金额
              notSmallChange:0,
              payType:'现金',
              payType2:'支付宝',
              discount:100,
              remark:'',
              remarks: '',
              showUnit:false,
              parentData:{gatheringShow:false,showCashResult:false,pay1Money:0,pay2Money:0,orderId:''},
              orderNumber:'',
              customerName:'',
              isCash:false
            };
        },
        computed: {
          totalMoney(){
            return parseFloat(parseFloat(this.parentData.pay1Money).toFixed(2)+parseFloat(this.parentData.pay2Money).toFixed(2)).toFixed(2);
          },
          debtMony(){
            if((this.paymoney-this.parentData.pay1Money-this.parentData.pay2Money)==0){
              return 0;
            }else {
              return parseFloat( this.paymoney-this.parentData.pay1Money-this.parentData.pay2Money).toFixed(2);
            }
          }
        },  //计算属性
        created() {
          this.initData();
        },   //创建
        mounted() {
        },   //挂载
        methods: {
          initData(){
            this.parentData.orderId=this.$route.query.saleOrderId;//订单Id
            getSellOrderById(this.parentData.orderId).then(response=>{
              console.log(response)
              this.item = response.data;
              this.orderNumber= response.data.orderNumber;
              this.customerName= response.data.customerName;
              this.remarks = response.data.remarks;
              this.sumPrice=parseFloat(response.data.sumPrice).toFixed(2);
              this.realPay=parseFloat(response.data.realPay).toFixed(2);
              this.paymoney=parseFloat(response.data.toBePaid).toFixed(2);
            },error=>{
              Toast.clear();
              Toast({
                type:'text',
                position: 'middle',
                message: error==null?"系统异常":error.msg
              });
            });
          },
          toGatheringPage(){
            if(this.parentData.pay2Money!=0&&this.parentData.pay1Money!=0){
              pay(
                this.parentData.orderId,
                {
                  realPay:this.parentData.pay1Money,
                  payType:1
                }).then(
                response=>{
                  this.parentData.gatheringShow=true;
                  this.parentData.showCashResult=true;
                },error=>{
                  Toast.clear();
                  Toast({
                    type:'text',
                    position: 'middle',
                    message: error==null?"系统异常":error.msg
                  });
                }
              );
            }else if(this.parentData.pay1Money!=0){
              pay(
                this.parentData.orderId,
                {
                realPay:this.parentData.pay1Money,
                payType:1
              }).then(
                response=>{
                  this.initData();
                  if(this.parentData.pay1Money<this.paymoney){             
                    Toast({
                      position: 'bottom',
                      message: '支付成功！尚欠款'+(parseFloat(this.paymoney-this.parentData.pay1Money).toFixed(2)).toString()
                    });
                  }else if(this.parentData.pay1Money==this.paymoney){
                    Toast({
                      position: 'bottom',
                      message: '支付成功！'
                    });
                  }
                },error=>{
                  Toast.clear();
                  Toast({
                    type:'text',
                    position: 'middle',
                    message: error==null?"系统异常":error.msg
                  });
                }
              );
            }else if(this.parentData.pay1Money==0){
              this.parentData.gatheringShow=true;
            }

          },
          computPay1Money(){
            this.parentData.pay1Money=this.paymoney-this.notSmallChange;
            this.parentData.pay2Money=0;
          },
          computPay2Money(){
            this.parentData.pay2Money=this.paymoney-this.notSmallChange-this.parentData.pay1Money;
          },
          showUnitPay(){
            this.parentData.pay2Money=0;
            this.showUnit=!this.showUnit;
          },
          confirmReceipt() {
            confirmReceiptById(this.item.id).then(
                response=>{
                  this.initData();
                  Toast.clear();
                  Toast({
                    type:'text',
                    position: 'middle',
                    message: response==null?"系统异常":response.msg
                  });
                },error=>{
                  Toast.clear();
                  Toast({
                    type:'text',
                    position: 'middle',
                    message: error==null?"系统异常":error.msg
                  });
                }
              );
          },
          closeOrder() {
            closeSoById(this.item.id).then(
                response=>{
                  this.initData();
                  Toast.clear();
                  Toast({
                    type:'text',
                    position: 'middle',
                    message: response==null?"系统异常":response.msg
                  });
                },error=>{
                  Toast.clear();
                  Toast({
                    type:'text',
                    position: 'middle',
                    message: error==null?"系统异常":error.msg
                  });
                }
              );
          }
        },   //方法
        watch: {}      //监听
    }
</script>

<style scoped>
  .showunit{
    background: red!important;
  }
</style>
