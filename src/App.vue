<template>
  <div id="app">
    <HelloWorld />
    <time-zone-selector />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TimeZoneSelector from './components/TimeZoneSelector.vue'
// import vSelect from '../node_modules/vue-select/src/components/Select.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    TimeZoneSelector,
    // vSelect
  },
  // data() {
  //   return {
  //     options: this.$root.$on('zoneList', this.options)
  //   }
  // }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
