<template>
  <div id="app">
    <igpic />
  </div>
</template>

<script>
import igpic from '@/components/igpic.vue';
export default {
  name: 'app',
  components: {
    igpic
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
