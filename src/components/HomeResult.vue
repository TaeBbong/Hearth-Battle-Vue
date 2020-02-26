<template>
  <div>
    <div>{{results}}</div>
    <canvas id="canvas" ref="canvas" width="500" height="300"></canvas>
  </div>
</template>

<script>
export default {
  props: ["results"]
};
</script>

<style>
</style>