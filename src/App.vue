<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
  *{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: '微软雅黑';
  }
  ul,li{
    list-style: none;
  }
  a{
    text-decoration: none;
  }
  html,body{
    height: 100%;
    width: 100%;
    background: #ffffff;
  }
</style>
