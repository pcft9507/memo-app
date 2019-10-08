<template>
  <div id="app2">
  </div>
</template>

<script>
    function printMessage(elementId, format, message) {
      document.querySelector('#${elementId}').innerHTML = '<${format}>${message}</${format}>';
    }
    printMessage('msg', 'h1', 'Hello World');

export default {
  name: 'app2',
  components: {
    AppHeader,
    MemoApp
  }
};
</script>

<style>
  @import "./styles/reset.css";

  #app {
    width: 560px;
    margin: 0 auto;
  }
</style>
