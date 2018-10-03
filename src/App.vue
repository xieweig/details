<template>
  <div id="app">
<!--    <div id="nav">
      <router-link to="/">toHome</router-link> |
      <router-link to="/about">toAbout</router-link> |
      <router-link to="/first">toFirst</router-link> |
      <router-link to="/second">toSecond</router-link> |
      <router-link to="/third">toThird</router-link> |
    </div>-->
    <div>
      <el-menu mode="horizontal" class="el-menu" background-color="#1866aa"
               router="true" :default-active="$router.path">
        <el-menu-item index="/">主页</el-menu-item>
        <el-menu-item index="/first">第一页</el-menu-item>
        <el-menu-item index="/second">第二页</el-menu-item>
        <el-menu-item index="/third">第三页</el-menu-item>

      </el-menu>
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
