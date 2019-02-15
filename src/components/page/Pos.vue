<template>
  <div class="pos">
    <el-row>
      <el-col :span="7" class="pos-order" id="order-list">
        <el-tabs type="border-card">
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border center style="width:100%;">
              <el-table-column prop="goodsName" label="商品名称" align="center"></el-table-column>
              <el-table-column prop="count" label="数量" width="50" align="center"></el-table-column>
              <el-table-column prop="price" label="金额" width="70" align="center"></el-table-column>
              <el-table-column prop="操作" fixed="right" label="操作" align="center">
                  <!-- <template scope>
                    <el-button type="text" size="small">删除</el-button>
                    <el-button type="text" size="small">增加</el-button> -->
                  <template scope="scope">
                    <el-button type="text" size="small" @click = "del(scope.row)">删除</el-button>
                    <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                     <!-- 注意： addOrderList(scope.row)  scope 作用域 获取 里面的一行数据  Element规定 -->
                  </template>
              </el-table-column>
            </el-table>
            <div class="">
              数量：{{totalCount}} ------ 金额：{{totalMoney}}
            </div>
            <div class="table-btn">
              <el-button type="warning" >挂单</el-button>
              <el-button type="danger" @click='delAll()'>删除</el-button>
              <el-button type="success" @click= "checkout()">结账</el-button>
            </div>
         </el-tab-pane>
         <el-tab-pane label="挂单">
            挂单
         </el-tab-pane>
         <el-tab-pane label="外卖">
            外卖
         </el-tab-pane>
      </el-tabs>
      </el-col>
      <el-col :span="17">
        <div class="often-goods">
           <div class="title">
             常用商品
           </div>
           <div class="often-goods-list">
             <ul>
               <!-- <li v-for='list in oftenGoods'>
                 <span>{{list.goodsName}}</span>
                 <span class="o-price">￥{{list.price}}元</span> -->
               <li v-for='item in oftenGoods' @click="addOrderList(item)">
                 <span>{{item.goodsName}}</span>
                 <span class="o-price">￥{{item.price}}元</span>
               </li>
             </ul>
           </div>
        </div>
       <div class="goods-type">
           <el-tabs type="border-card">
               <el-tab-pane label="汉堡">
                   <div class="">
                      <ul class='cookList'>
                        <li v-for="item in type0Goods" @click="addOrderList(item)">
                            <span class="foodImg"><img :src="item.goodsImg" width="100%"/></span>
                            <span class="foodName">{{item.goodsName}}</span>
                            <span class="foodPrice">￥{{item.price}}元</span>
                        </li>
                      </ul>
                   </div>
               </el-tab-pane>
              <el-tab-pane label="小食">
                <div class="">
                   <ul class='cookList'>
                     <li v-for="item in type1Goods" @click="addOrderList(item)">
                         <span class="foodImg"><img :src="item.goodsImg" width="100%"/></span>
                         <span class="foodName">{{item.goodsName}}</span>
                         <span class="foodPrice">￥{{item.price}}元</span>
                     </li>
                   </ul>
                </div>
               </el-tab-pane>
               <el-tab-pane label="饮料">
                 <div class="">
                    <ul class='cookList'>
                      <li v-for="item in type2Goods" @click="addOrderList(item)">
                          <span class="foodImg"><img :src="item.goodsImg" width="100%"/></span>
                          <span class="foodName">{{item.goodsName}}</span>
                          <span class="foodPrice">￥{{item.price}}元</span>
                      </li>
                    </ul>
                 </div>
               </el-tab-pane>
               <el-tab-pane label="套餐">
                 <div class="">
                    <ul class='cookList'>
                      <li v-for="item in type3Goods" @click="addOrderList(item)">
                          <span class="foodImg"><img :src="item.goodsImg" width="100%"/></span>
                          <span class="foodName">{{item.goodsName}}</span>
                          <span class="foodPrice">￥{{item.price}}元</span>
                      </li>
                    </ul>
                 </div>
               </el-tab-pane>
           </el-tabs>
       </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios'//引入axios
export default {
  name: 'Pos',
  data(){
    return {
      tableData: [],//订单列表的值
      oftenGoods:[],//常用商品
      type0Goods:[],//商品分类
      type1Goods:[],
      type2Goods:[],
      type3Goods:[],
      totalMoney:0,
      totalCount:0
    }
  },
  mounted:function(){//挂载上之后执行
    var orderHeight = document.body.clientHeight;
    //console.log(orderHeight);
    document.getElementById("order-list").style.height=orderHeight + 'px';
  },
  created(){
    //读取常用商品列表
    axios.get('http://jspang.com/DemoApi/oftenGoods.php')
    .then(response=>{
      //console.log(response.data);
      this.oftenGoods = response.data;
    }).catch(error=>{
      //console.log(error);
      alert('获取数据失败！')
    })
    //读取分类商品列表
    axios.get('http://jspang.com/DemoApi/typeGoods.php')
    .then(response=>{
      //console.log(response.data);
      this.type0Goods = response.data[0];
      this.type1Goods = response.data[1];
      this.type2Goods = response.data[2];
      this.type3Goods = response.data[3];
    }).catch(error=>{
        //console.log(error);
        alert('获取数据失败！')
    })
  },
  methods:{
    addOrderList(item){
      let isHave=false;
      //判断商品是否已经存在于订单列表中
      for(let i=0;i<this.tableData.length;i++){
        //console.log(this.tableData.goodsId);
        if(this.tableData[i].goodsId == item.goodsId){  //判断tableData力有没有这个 id
          isHave = true;//存在
        }
      }
      //根据isHave的值判断订单列表中是否已经有此商品
       if(isHave){
         //存在就进行数量添加
         let arr = this.tableData.filter(o =>o.goodsId == item.goodsId);
         arr[0].count++;
         //console.log(arr);
       }else{
         //不存在就推入数组
         let newGoods = {goodsId:item.goodsId,goodsName:item.goodsName,price:item.price,count:1};
         this.tableData.push(newGoods);
       }
      //进行数量和价格的汇总计算
      this.getAllMoney();
    },
    //删除单个商品
    del(goods){
      this.tableData = this.tableData.filter(o => o.goodsId != goods.goodsId);
      //过滤出除了 goods.id 里 之外的tableData的值
      this.getAllMoney();
    },
    //汇总数量和金额
    getAllMoney(){
      this.totalCount=0; //汇总数量清0
      this.totalMoney=0;//金额清0
      if(this.tableData){
        this.tableData.forEach((element)=>{
          this.totalCount += element.count;
          this.totalMoney = this.totalMoney + (element.price * element.count);
         })
      }
    },
    //删除所有商品
    delAll(){
      this.tableData = [];
      this.totalCount = 0;
      this.totalMoney = 0;
    },
    //结账  模拟结账
    checkout(){
      if(this.totalMoney != 0){
        this.tableData = [];
        this.totalCount = 0;
        this.totalMoney = 0;
        this.$message({
          message: "结账成功，感谢你又为店里做出了一份贡献！",
          type:"success"
        })
      }else{
        this.$message.error("不能空结！")
      }
    }
  }
}
</script>
<style scoped>
.pos-order{
  background: #f9fafc;
  border-right:1px solid #c0c0cc;
}
.table-btn{
  margin-top: 10px;
}
.title{
  height: 20px;
  border-bottom:1px solid #D3DCE6;
  background-color: #F9FAFC;
  padding:10px;
}
.often-goods-list ul li{
  list-style: none;
  float:left;
  border:1px solid #E5E9F2;
  padding:10px;
  margin:5px;
  background-color:#fff;
  cursor: pointer;
}
.o-price{
  color:#58B7FF;
}
.goods-type{
  clear: both;
}
.cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auot;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
      cursor: pointer;
   }
   .cookList li span{

        display: block;
        float:left;
   }
   .foodImg{
       width: 40%;
   }
   .foodName{
       font-size: 18px;
       padding-left: 10px;
       color:brown;

   }
   .foodPrice{
       font-size: 16px;
       padding-left: 10px;
       padding-top:10px;
   }

</style>
