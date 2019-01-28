<template>
  <div id="app">
    <HelloWorld />
    <v-select :options="['foo','bar']"></v-select>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import vSelect from '../node_modules/vue-select/src/components/Select.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    vSelect
  }
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
