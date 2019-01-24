<template>
  <div id="app">
    <span>
    {{ timestamp }}
    </span>
    <button @click="unixTime()">Show me the time</button>
    <button @click="timestampToHour()">Show me the hours</button>
    </div>
</template>
<script>
import axios from "axios";

export default {
  // el: "#app",
  data() {
    return {
      info: null,
      timestamp: null,
      hours: null
    };
  },
  mounted() {
    axios
      .get("http://api.timezonedb.com/v2.1/list-time-zone?key=PVVEZXX7L9E5&format=json&country=NZ")
      // .then(response => (console.log(response.data.zones[0].timestamp)))
      // .then(response => (this.data = response.data))
      .then(response => (this.timestamp = response.data.zones[0].timestamp))
  },
  methods: {
    unixTime: function (timestamp) {
      console.log(this.timestamp);
    },
    timestampToHour: function (timestamp) {
       const timeToHour = function () {
        (this.hours * 1000).getHours();
      }
      console.log(timeToHour);
    }
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
