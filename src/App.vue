<template>
  <div id="app">
    <Composition />
    <!-- <div>{{ `x坐标：${x},y坐标:${y}` }}</div> -->
    <Selected3 />
  </div>
</template>

<script>
import Composition from './components/Composition'
import { useMousePosition } from './tools/test'
// import Selected2 from './components/Selected2'
import Selected3 from './components/Selected3'
export default {
  components: {
    Composition,
    // Selected2,
    Selected3
  },
  setup() {
    const { x, y } = useMousePosition()
    return { x, y }
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
</style>
