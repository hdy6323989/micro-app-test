<template>
<div>
  <micro-app name='app1' url='http://127.0.0.1:8081/' baseroute='/main/app1' keep-alive></micro-app>
</div>
</template>

<script>
export default {
  created(){
    /* 0.X版本下功能正常 */
    //window.dispatchEvent(new PopStateEvent('popstate', { state: history.state }))
      
    /* 1.0版本需要延迟设置 */
    /* setTimeout(() => {
      window.dispatchEvent(new PopStateEvent('popstate', { state: history.state }))
    }, 300); */

    /* 延时小于200 ,用以下方法在已经缓存的情况下切换子应用，子应用会出现bug，关闭的虚拟路由系统会生效*/
    /* setTimeout(() => {
      window.history.replaceState(history.state, '', '/main'+this.$route.fullPath)
      window.dispatchEvent(new PopStateEvent('popstate', { state: history.state }))
    }, 0); */

    /* 最后发现，如果不replaceState，延时过小就不会出现上述BUG */
    setTimeout(() => {
      window.dispatchEvent(new PopStateEvent('popstate', { state: history.state }))
    }, 0);
  },
  watch:{
    $route(){
      window.dispatchEvent(new PopStateEvent('popstate', { state: history.state }))
    },
  }
}
</script>

<style>

</style>