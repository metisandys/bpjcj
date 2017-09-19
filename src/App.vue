<template>
  <div id="app">
    <header-v></header-v>
    <content-v></content-v>
    <content-v></content-v>
  </div>
</template>

<script>
  import header from './components/head.vue';
  import content from './components/content.vue';

  export default {
    data() {
      return {
        
      }
    },
    components: {
      'header-v': header,
      'content-v': content
    }
  }
</script>

<style scoped>
  #app{
    padding-left: 20px;
  }
</style>
