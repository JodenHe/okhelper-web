<template>
  <div>
      <div style="border-bottom: 1px dashed #F2F2F2;height: 26px;line-height: 26px;">
        <span style="font-weight: bolder;">{{parentData.productName}}<span v-if="parentData.productNumber!=null&&parentData.productNumber!=''" style="color: #108ee9">({{parentData.productNumber}})</span></span>
        <!--<i style="color: #108ee9;margin-left: 15px;" class="ion-edit"></i>-->
      </div>
      <div style="border-bottom: 1px dashed #F2F2F2">
        <ul style="list-style: none;height: 36px;line-height: 36px;width: 100%;font-size: 12px;">
          <li style="display: block;float: left;width: 10%;">
            <div v-if="editText=='编辑'">
              <div @click="showNoteOrPrice(1)" style="height: 26px;width: 26px;border-radius: 13px;color:white;background: #F2F2F2;font-size:10px;text-align: center;margin-top: 5px;line-height: 24px;">备</div>
            </div>
            <div v-else>
              <div @click="deleteProduct" style="height: 26px;width: 26px;border-radius: 13px;color:white;background: red;font-size:10px;text-align: center;margin-top: 5px;line-height: 26px;">一</div>
            </div>
          </li>
          <li style="display: block;float: left;width: 20%;text-align: center;">
            <div><span v-if="productAttribute.productColor!=null&&productAttribute.productColor!=''">{{productAttribute.productColor}}</span><span v-else>均色</span></div>
          </li>
          <li style="display: block;float: left;width: 20%;text-align: center;">
            <div><span v-if="productAttribute.productSize!=null&&productAttribute.productSize!=''">{{productAttribute.productSize}}</span><span v-else>均码</span></div>
          </li>
          <li style="display: block;float: left;width: 20%;text-align: center;">
            <div>￥{{discountPrice}}</div>
          </li>
          <li style="display: block;float: left;width: 20%;text-align: center;">
            <div>{{parentData.productCount}}</div>
          </li>
          <li style="display: block;float: left;width: 10%;color: #575757;">
            <i @click="showNoteOrPrice(2)" :class="[isPriceOpen?'ion-chevron-up':'ion-chevron-down']"></i>
          </li>
        </ul>
        <div v-show="isPriceOpen">
          <ul style="list-style: none;background: #F2F2F2;width: 100%;height:50px;padding-top:5px;text-align: center;">
            <li class="sell-table-price-detail-open-li">
              <div>单价</div>
              <input class="sell-table-price-detail-open-li-input" type="number" v-model="parentData.retailPrice" />
            </li>
            <li class="sell-table-price-detail-open-li">
              <div>折扣(%)</div>
              <input @blur="minMaxDiscount" class="sell-table-price-detail-open-li-input" type="number" v-model="parentData.discounts"/>
            </li>
            <li class="sell-table-price-detail-open-li">
              <div>折后价</div>
              <input class="sell-table-price-detail-open-li-input" disabled type="number" v-model="discountPrice"/>
            </li>
            <li class="sell-table-price-detail-open-li">
              <div>数量</div>
              <input @blur="minMaxCount" class="sell-table-price-detail-open-li-input" type="number" v-model="parentData.productCount"/>
            </li>
          </ul>
        </div>
        <div v-show="isNoteOpen&&editText=='编辑'" style="width: 100%;height: 40px;border-top: 1px #F2F2F2 dashed;line-height: 40px;font-size: 16px;margin-top: 5px;margin-bottom: 5px;">
          <div style="width:20%;height: 100%;float: left;text-align: center;color: #888888">备注</div>
          <input style="border-bottom:1px solid #108ee9;width: 70%;display: inline;height: 34px;margin-top:3px;float: left;" type="text" v-model="parentData.productNotes"/>
        </div>
      </div>
  </div>
</template>

<script>
    import { Toast } from 'vant';
    export default {
        mixins: [],     //混合
        props:{
          parentData:{},
          // productId:{},
          // productName:{},
          // productNumber:{},
          // productDetails:{},
          // discounts:{default:100},
          editText:{},
          // productCount:{default:1},
          // retailPrice:{},
          // productNotes:{}
        },
        components: {
        },//注册组件
        data() {         //数据
            return {
              isNoteOpen:false,
              isPriceOpen:false

            };
        },
        computed: {
          discountPrice(){
            return parseFloat(this.parentData.retailPrice*this.parentData.discounts/100).toFixed(2);
          },
          productAttribute(){
            return 1;
            // return JSON.parse(this.parentData.productDetails);
          }
        },  //计算属性
        created() {
          // alert(1)
          // console.log(this.parentData);
        },   //创建
        mounted() {
        },   //挂载
        methods: {
          showNoteOrPrice(n){
            switch (n){
              case 1:this.isNoteOpen=!this.isNoteOpen;this.isPriceOpen=false;break;
              case 2:this.isNoteOpen=false;this.isPriceOpen=!this.isPriceOpen;break;
              default:this.isNoteOpen=!this.isNoteOpen;this.isPriceOpen=false;
            }
          },
          deleteProduct(){
            this.$emit('deleteProduct',this.parentData.id);
          },
          minMaxCount(){
            if(this.parentData.productCount>this.parentData.salesStock){
                Toast({
                  position: 'middle',
                  message: '销售数量不能大于库存'
                });
              this.parentData.productCount=this.parentData.salesStock;
              return;
            }

            if(this.parentData.productCount<1){
              Toast({
                position: 'middle',
                message: '销售数量不能小于1'
              });
              this.parentData.productCount=1;
            }
          },
          minMaxDiscount(){
            if(this.parentData.discounts>100){
                Toast({
                  position: 'middle',
                  message: '折扣率不能大于100'
                });
              this.parentData.discounts=100;
            }

            if(this.parentData.discounts<1){
              Toast({
                position: 'middle',
                message: '折扣率不能小于1'
              });
              this.parentData.discounts=1;
            }
          }
        },   //方法
        watch: {
          // 'parentData.productCount':function(val,olVal){
          //
          // }
        }      //监听
    }
</script>

<style scoped>
  .sell-table-price-detail-open-li{
    display: block;float: left;width: 25%;padding-left: 10px;padding-right: 10px;
  }
  .sell-table-price-detail-open-li-input{
    height: 20px;width: 100%;margin-top: 2px;border-bottom: 1px solid #108ee9;
  }
</style>
