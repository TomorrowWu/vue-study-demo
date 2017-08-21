<template>
  <div class="pos">
    <!--Hello Pos Demo!-->
    <el-row>
      <!--el-col这一类型组件,是怎么将css和html封装成一个组件供使用的-->
      <el-col :span='7' class="pos-order" id="order-list">
        我是订单栏
      </el-col>
      <el-col :span="17">
        我是产品栏
      </el-col>
    </el-row>
  </div>
</template>

<script>
  export default {
    name: 'Pos',
    mounted: function () {
      var orderHeight = document.body.clientHeight
      console.log(orderHeight)
      document.getElementById('order-list').style.height = orderHeight = orderHeight + 'px'
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
</style>
