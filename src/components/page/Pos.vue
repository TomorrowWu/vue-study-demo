<template>
  <div class="pos">
    <!--Hello Pos Demo!-->
    <el-row>
      <el-col :span='7' class="pos-order" id="order-list">
        我是订单栏
      </el-col>
      <el-col>
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
    height: 100%;
  }
</style>
