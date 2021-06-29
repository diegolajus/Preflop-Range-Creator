<template>
  <div id="app">
    <div class="site-container">
      <ColorPicker/>
      <HelloWorld/>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ColorPicker from './components/ColorPicker.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,ColorPicker,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body{
  background: #0f0c29;  /* fallback for old browsers */
background: -webkit-linear-gradient(to right, #24243e, #302b63, #0f0c29);  /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to right, #24243e, #302b63, #0f0c29); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

}
.site-container{
  display: flex;
  justify-content: space-around;
}
</style>

