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
  components: {
    AppHeader,
    AppMain
  },
  //props: {searchText: '',}
}


</script>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  background-color: #141414;
  color: white;
font-family: "Comic Sans MS", "Comic Sans", cursive;
}
</style>