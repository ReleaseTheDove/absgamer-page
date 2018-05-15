<template>
  <div id="app">
    <!-- <ul>
      <li><router-link to="/helloworld">helloworld</router-link></li>
      <li><router-link to="/h1">h1</router-link></li>
    </ul> -->
    <div class="app_header"></div>
    <div class="app_main">
      <router-view/>
    </div>
    <div class="app_footer"></div>
  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld'
  import home from './components//home/home'

  export default {
    name: 'App',
    components: {
      HelloWorld,
      home
    }
  }
</script>

<style>
#app {
  /* 默认 */
  /* font-family: 'Avenir', Helvetica, Arial, sans-serif; */
  /* 简书 */
  font-family: "lucida grande", "lucida sans unicode", lucida, helvetica, "Hiragino Sans GB", "Microsoft YaHei", "WenQuanYi Micro Hei", sans-serif;
  /* 小米 */
  /* font: 14px/1.5 "Helvetica Neue",Helvetica,Arial,"Microsoft Yahei","Hiragino Sans GB","Heiti SC","WenQuanYi Micro Hei",sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #f0f0f0;
}
#app .app_header {
  height: 50px;
}
#app .app_main {
  width: 1000px;
  min-height: 1200px;
  margin: 0 auto;
  padding: 20px;
  background-color: white;
  box-shadow: 0 10px 30px 0 rgba(0,0,0,.7)
}
#app .app_footer {
  height: 50px;
}
</style>
