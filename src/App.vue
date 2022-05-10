<template>
  <div id="app">
    <app-header />
    <app-main />
  </div>
</template>

<script>
import AppHeader from './components/header.vue'
import AppMain from './components/main.vue'

export default {
  name: 'App',
  components:{
    AppHeader,
    AppMain
  }
}


</script>

<style lang="scss">
@import "src/styles/general.scss";
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
      background-color: #1E2D3B;
}
</style>