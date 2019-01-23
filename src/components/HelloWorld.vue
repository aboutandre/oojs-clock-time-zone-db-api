<template>
  <div id="app">{{ info }}</div>
</template>
<script>
import axios from "axios";

export default {
  // el: "#app",
  data() {
    return {
      info: null
    };
  },
  mounted() {
    axios
      .get("http://api.timezonedb.com/v2.1/list-time-zone?key=PVVEZXX7L9E5&format=json&country=NZ")
      .then(response => (this.info = response.data.status))
      .then(response => (console.log(response.data)));
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
