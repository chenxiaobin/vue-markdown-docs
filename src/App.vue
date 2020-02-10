<template>
  <div id="app">
    <test></test> 
  </div>
</template>

<script>
import Test from './examples/test'
export default {
  name: 'App',
  components: {
    Test
  }
}
</script>

<style>
html, body{
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0; 
}
#app {
  width: 100%;
  height: 100%;
}
</style>
