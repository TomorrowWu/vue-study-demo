<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <!--<i class="icon iconfont icon-dianpu"></i>-->
    <!--<i class="icon iconfont icon-gongnengjianyi"></i>-->
    <!-- <i class="icon iconfont icon-shouji"></i> -->

    <!--左侧导航-->
    <left-nav></left-nav>

    <div class="main">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import leftNav from '@/components/common/leftNav'
export default {
  name: 'app',
  components: {
    leftNav
  }
}
</script>

<style>
#app {
  font-family: 'Microsoft YaHei','Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  /*color: #2c3e50;*/
  /*color: #980988;*/
}

.main {
  float: left;
  width: 95%;
  background-color: #EFF2F7;
  height: 100%;
  overflow: hidden;
}
</style>
