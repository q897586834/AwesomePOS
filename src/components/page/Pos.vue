<template>
  <div class="pos">
    <div>
      <el-row>
        <el-col :span="7" class="pos-order" id="order-list">
          <el-tabs>
            <el-tab-pane label="点餐">
              <el-table :data="tableData" border style="width: 100%;font-size:1rem">
                <el-table-column prop="goodsName" label="商品名称" style="width: 25%"></el-table-column>
                <el-table-column prop="count" label="数量" style="width: 25%"></el-table-column>
                <el-table-column prop="price" label="金额" style="width: 25%"></el-table-column>
                <el-table-column label="操作" width="100" fixed="right">
                  <template slot-scope="scope">
                    <el-button
                      type="text"
                      size="small"
                      style="font-size:.5rem"
                      @click="delSingleGoods(scope.row)"
                    >删除</el-button>
                    <el-button
                      type="text"
                      size="small"
                      style="font-size:.5rem"
                      @click="addOrderList(scope.row)"
                    >增加</el-button>
                  </template>
                </el-table-column>
              </el-table>
              <div class="totalDiv">
                <small>数量</small>
                :{{totalCount}} &nbsp;&nbsp;&nbsp;&nbsp;
                <small>金额</small>
                :{{totalMoney}}元
              </div>
              <div class="div-btn">
                <el-button type="warning">挂单</el-button>
                <el-button type="danger" @click="delAllGoods()">删除</el-button>
                <el-button type="success" @click="checkout()">结账</el-button>
              </div>
            </el-tab-pane>
            <el-tab-pane label="挂单">挂单</el-tab-pane>
             <!-- <el-table :data="tableData" border style="width: 100%;font-size:1rem">
                <el-table-column prop="goodsName" label="第一单" style="width: 25%"></el-table-column>
                <el-table-column prop="price" label="金额" style="width: 25%"></el-table-column>
                <el-table-column label="操作" width="100" fixed="right"></el-table-column>
              </el-table> -->
            <el-tab-pane label="外卖">外卖</el-tab-pane>
          </el-tabs>
        </el-col>
        <!--商品展示-->
        <el-col :span="17">
          <div class="often-goods">
            <div class="title">常用商品</div>
            <div class="often-goods-list">
              <ul>
                <li v-for="(type0,i) in type0Goods " :key="i" @click="addOrderList(type0)">
                  <span>{{type0.goodsName}}</span>
                  <span class="o-price">${{type0.price}}</span>
                </li>
              </ul>
            </div>
          </div>
          <div class="goods-type">
            <el-tabs style="font-size:1rem">
              <el-tab-pane label="汉堡">
                <div>
                  <ul class="cookList">
                    <li v-for="(type0,i) in type0Goods " :key="i" @click="addOrderList(type0)">
                      <span class="foodImg">
                        <img :src="type0.goodsImg" width="100%">
                      </span>
                      <span class="foodName">{{type0.goodsName}}</span>
                      <br>
                      <span class="foodPrice">￥{{type0.price}}元</span>
                    </li>
                  </ul>
                </div>
              </el-tab-pane>
              <el-tab-pane label="小食">
                <div>
                  <ul class="cookList">
                    <li v-for="(type0,i) in type1Goods " :key="i" @click="addOrderList(type0)">
                      <span class="foodImg">
                        <img :src="type0.goodsImg" width="100%">
                      </span>
                      <span class="foodName">{{type0.goodsName}}</span>
                      <br>
                      <span class="foodPrice">￥{{type0.price}}元</span>
                    </li>
                  </ul>
                </div>
              </el-tab-pane>
              <el-tab-pane label="饮料">
                <div>
                  <ul class="cookList">
                    <li v-for="(type0,i) in type2Goods " :key="i" @click="addOrderList(type0)">
                      <span class="foodImg">
                        <img :src="type0.goodsImg" width="100%">
                      </span>
                      <span class="foodName">{{type0.goodsName}}</span>
                      <br>
                      <span class="foodPrice">￥{{type0.price}}元</span>
                    </li>
                  </ul>
                </div>
              </el-tab-pane>
              <el-tab-pane label="套餐">
                <div>
                  <ul class="cookList">
                    <li v-for="(type0,i) in type3Goods " :key="i" @click="addOrderList(type0)">
                      <span class="foodImg">
                        <img :src="type0.goodsImg" width="100%">
                      </span>
                      <span class="foodName">{{type0.goodsName}}</span>
                      <br>
                      <span class="foodPrice">￥{{type0.price}}元</span>
                    </li>
                  </ul>
                </div>
              </el-tab-pane>
            </el-tabs>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "pos",
  data() {
    return {
      tableData: [],
      oftenGoods: [],
      type0Goods: [],
      type1Goods: [],
      type2Goods: [],
      type3Goods: [],
      totalMoney: 0,
      totalCount: 0
    };
  },
  created() {
    axios
      .get(
        "https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods"
      )
      .then(response => {
        //console.log(response);
        this.oftenGoods = response.data;
      })
      .catch(error => {
        //console.log(error);
        alert("网络错误，不能访问");
      }),
      axios
        .get(
          "https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods"
        )
        .then(response => {
          //console.log(response);
          this.type0Goods = response.data[0];
          this.type1Goods = response.data[1];
          this.type2Goods = response.data[2];
          this.type3Goods = response.data[3];
        })
        .catch(error => {
          //console.log(error);
          alert("网络错误，不能访问");
        });
  },
  mounted: function() {
    var orderHeight = document.body.clientHeight;
    document.getElementById("order-list").style.height = orderHeight + "px";
  },

  methods: {
    //结账
    checkout() {
      if (this.totalCount != 0) {
        this.tableData = [];
        this.totalCount = 0;
        this.totalMoney = 0;
        this.$message({
          message: "结账成功，感谢你又为店里出了一份力!",
          type: "success"
        });
      } else {
        this.$message.error("不能空结。老板了解你急切的心情！");
      }
    },
    //添加订单列表的方法
    addOrderList(goods) {
      this.totalCount = 0; //汇总数量清0
      this.totalMoney = 0;
      let isHave = false;
      //判断是否这个商品已经存在于订单列表
      for (let i = 0; i < this.tableData.length; i++) {
        console.log(this.tableData[i].goodsId);
        if (this.tableData[i].goodsId == goods.goodsId) {
          isHave = true; //存在
        }
      }
      //根据isHave的值判断订单列表中是否已经有此商品
      if (isHave) {
        //存在就进行数量添加
        let arr = this.tableData.filter(o => o.goodsId == goods.goodsId);
        arr[0].count++;
        //console.log(arr);
      } else {
        //不存在就推入数组
        let newGoods = {
          goodsId: goods.goodsId,
          goodsName: goods.goodsName,
          price: goods.price,
          count: 1
        };
        this.tableData.push(newGoods);
      }
      this.getAllMoney();
    },
    //删除单个商品
    delSingleGoods(goods) {
      console.log(goods);
      this.tableData = this.tableData.filter(o => o.goodsId != goods.goodsId);
      this.getAllMoney();
    },
    delAllGoods() {
      this.tableData = [];
      this.totalMoney = 0;
      this.totalCount = 0;
    },
    //汇总数量和金额
    getAllMoney() {
      this.totalCount = 0;
      this.totalMoney = 0;
      if (this.tableData) {
        //进行数量和价格的汇总计算
        this.tableData.forEach(element => {
          this.totalCount += element.count;
          this.totalMoney = this.totalMoney + element.price * element.count;
        });
      }
    }
  }
};
</script>
<style scoped>
.pos-order {
  background-color: #f9fafc;
  border-right: 1px solid #c0ccda;
  float: left;
}
.div-btn {
  margin-top: 30px;
  text-align: center;
}
.title {
  height: 20px;
  border-bottom: 1px solid #d3dce6;
  background-color: #f9fafc;
  padding: 10px;
}
.often-goods-list ul li {
  list-style: none;
  float: left;
  border: 1px solid #e5e9f2;
  padding: 10px;
  margin: 5px;
  background-color: #fff;
  cursor: pointer;
}
.o-price {
  color: #58b7ff;
}
.goods-type {
  clear: both;
}
.cookList li {
  list-style: none;
  width: 23%;
  border: 1px solid #e5e9f2;
  height: auot;
  overflow: hidden;
  background-color: #fff;
  padding: 2px;
  float: left;
  margin: 2px;
  cursor: pointer;
}
.cookList li span {
  display: block;
  float: left;
}
.foodImg {
  width: 40%;
}
.foodName {
  font-size: 18px;
  padding-left: 10px;
  color: brown;
}
.foodPrice {
  font-size: 16px;
  padding-left: 10px;
  padding-top: 10px;
}
.totalDiv {
  background-color: #fff;
  padding: 10px;
  border-bottom: 1px solid #d3dce6;
  text-align: center;
}
</style>