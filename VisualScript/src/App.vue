<script lang="ts">
  import Node from './components/Node.vue'
  export default {
    components: {
      Node
    }
  }
</script>

<template>
  <div id="canvas">
    <Node />
  </div>
</template>

<style>
  #canvas {
    position: absolute;
  }
</style>