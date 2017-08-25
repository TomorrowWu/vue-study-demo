<template>
  <div class="pos">
    <!--Hello Pos Demo!-->
    <el-row>
      <!--el-col这一类型组件,是怎么将css和html封装成一个组件供使用的-->
      <el-col :span='7' class="pos-order" id="order-list">
        <el-tabs>
          <el-tab-pane label="点餐">
            <!--点餐-->
            <el-table :data="tableData" border style="width: 100%">
              <el-table-column prop="goodsName" label="商品名称"></el-table-column>
              <el-table-column prop="count" label="数量" width="50"></el-table-column>
              <el-table-column prop="price" label="金额" width="70"></el-table-column>
              <el-table-column label="操作" width="100" fixed="right">
                <template scope="scope">
                  <el-button type="text" size="small">删除</el-button>
                  <!--scope:作用域,可以取到这一行的数据-->
                  <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>

            <div class="totalDiv">
              <small>数量:</small>
              {{totalCount}}  &nbsp;&nbsp;&nbsp;&nbsp;
              <small>金额:</small>
              {{totalMoney}}元
            </div>

            <div class="div-btn">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger">删除</el-button>
              <el-button type="success">结账</el-button>
            </div>

          </el-tab-pane>
          <el-tab-pane label="挂单">
            挂单
          </el-tab-pane>
          <el-tab-pane label="外卖">
            外卖
          </el-tab-pane>
        </el-tabs>
        <!--我是订单栏-->
      </el-col>

      <el-col :span="17">
        <!--我是产品栏-->
        <div class="often-goods">
          <div class="title">常用商品</div>
          <div class="often-goods-list">
            <ul>
              <li v-for="goods in oftenGoods" @click="addOrderList(goods)">
                <span>{{goods.goodsName}}</span>
                <span class="o-price">¥{{goods.price}}元</span>
              </li>
            </ul>
          </div>
        </div>

        <div class="goods-type">
          <el-tabs>
            <el-tab-pane label="汉堡">
              <!--汉堡-->
              <div>
                <ul class='cookList'>
                  <li v-for="goods in type0Goods" @click="addOrderList(goods)">
                    <span class=" foodImg"><img :src="goods.goodsImg" width="100%"></span>
                    <span class="foodName">{{goods.goodsName}}</span>
                    <span class="foodPrice">￥{{goods.price}}元</span>
                  </li>
                </ul>
              </div>

            </el-tab-pane>
            <el-tab-pane label="小食">
              <!--小食-->
              <ul class='cookList'>
                <li v-for="goods in type1Goods" @click="addOrderList(goods)">
                  <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                  <span class="foodName">{{goods.goodsName}}</span>
                  <span class="foodPrice">￥{{goods.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="饮料">
              <!--饮料-->
              <ul class='cookList'>
                <li v-for="goods in type2Goods" @click="addOrderList(goods)">
                  <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                  <span class="foodName">{{goods.goodsName}}</span>
                  <span class="foodPrice">￥{{goods.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="套餐">
              <!--套餐-->
              <ul class='cookList'>
                <li v-for="goods in type3Goods" @click="addOrderList(goods)">
                  <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                  <span class="foodName">{{goods.goodsName}}</span>
                  <span class="foodPrice">￥{{goods.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>
          </el-tabs>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'Pos',
    data () {
      return {
        tableData: [],
        oftenGoods: [],
        type0Goods: [],
        type1Goods: [],
        type2Goods: [],
        type3Goods: [],
        totalMoney: 0,
        totalCount: 0
      }
    },
    created: function () {
      axios.get('http://jspang.com/DemoApi/oftenGoods.php')
        .then(response => {
          console.log(response)
          this.oftenGoods = response.data
        })
        .catch(error => {
          console.log(error)
          alert('网络错误,不能访问')
        })
//      读取分类商品列表
      axios.get('http://jspang.com/DemoApi/typeGoods.php')
        .then(response => {
          console.log(response)
          this.type0Goods = response.data[0]
          this.type1Goods = response.data[1]
          this.type2Goods = response.data[2]
          this.type3Goods = response.data[3]
        })
        .catch(error => {
          console.log(error)
          alert('网络错误，不能访问')
        })
    },
    mounted: function () {
      var orderHeight = document.body.clientHeight
      console.log(orderHeight)
      document.getElementById('order-list').style.height = orderHeight = orderHeight + 'px'
    },
    methods: {
      addOrderList (goods) {
        this.totalMoney = 0
        this.totalCount = 0
//        商品是否已存在订单列表中
        let isHave = false
        for (let i = 0; i < this.tableData.length; i++) {
          if (this.tableData[i].goodsId === goods.goodsId) {
            isHave = true
          }
        }
//        有->加数量
        if (isHave) {
//          改变列表中商品数量
          let arr = this.tableData.filter(o => o.goodsId === goods.goodsId)
          arr[0].count++
        } else {
          let newGoods = {goodsId: goods.goodsId, goodsName: goods.goodsName, price: goods.price, count: 1}
          this.tableData.push(newGoods)
        }

//        计算汇总金额和数量
        this.tableData.forEach((element) => {
          this.totalCount += element.count
          this.totalMoney += element.price * element.count
        })
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .pos-order {
    background-color: #F9FAFC;
    border-right: 1px solid #C0CCDA;
    /*在页面中使用了Element组件，这样他会自动给我们生产虚拟DOM，我们无法设置高度100%；*/
    height: 100%;
  }

  .div-btn {
    margin-top: 10px;
  }

  .title {
    height: 20px;
    border-bottom: 1px solid #d3dce6;
    background-color: #f9fafc;
    padding: 10px;
    text-align: left;
  }

  .often-goods-list ul li {
    list-style: none;
    float: left;
    border: 1px solid #e5e9f2;
    padding: 10px;
    margin: 10px;
    background-color: #fff;
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
    height: auto;
    /*规定当内容溢出元素框时发生的事情*/
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
    font-size: 16px;
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
  }
</style>
