<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <i class="icon iconfont icon-dianpu"></i>
    <i class="icon iconfont icon-gongnengjianyi"></i>
    <i class="icon iconfont icon-shouji"></i>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  color: #980988;
  margin-top: 60px;
}
</style>
