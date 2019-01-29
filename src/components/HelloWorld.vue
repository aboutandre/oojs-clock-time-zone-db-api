<template>
  <div id="app">
    <span>{{ locationData }}</span>
    <button @click="unixTime()">Show me the time</button>
    <button @click="timestampToHour()">Show me the hours</button>
    <span>This is formatted: {{ formatted }}</span>
  </div>
</template>
<script>
import axios from "axios";

export default {
  // el: "#app",
  data() {
    return {
      locationData: null,
      info: null,
      timestamp: null,
      hours: null,
      dst: null,
      formatted: null
    };
  },
  watch: {
    locationData: function() {
      this.timestamp = this.locationData.timestamp;
      this.timestampToHour();
      /**
       * I need to update all these paremeter using this watch.
       * I'll need to write computed (?) properties to deal with this.
       */
    },
    dst: function() {
      this.dst = this.locationData.dst;
    },
    // formatted: function() {
    //   this.formatted = this.locationData.formatted;
    // }
  },
  // watch: {
  //   locationTimestamp() {
  //     this.timestamp = this.locationData.zones[0].timestamp;
  //   }
  // },
  // computed: {
  //   locationTimestamp() {
  //     this.timestamp = this.locationData.zones[0].timestamp;
  //     // return this.timestamp;
  //   }
  // },
  mounted() {
    axios
      .get(
        "http://api.timezonedb.com/v2.1/get-time-zone?key=PVVEZXX7L9E5&format=json&by=zone&zone=Europe/Berlin"
      )
      // .then(response => (console.log(response.data.zones[0].timestamp)))
      // .then(response => (this.data = response.data))
      .then(response => (this.locationData = response.data));
  },
  methods: {
    unixTime() {
      console.log(this.timestamp);
      console.log(this.info);
    },
    date() {
      const thisTimeStamp = new Date(this.timestamp * 1000);
      return thisTimeStamp;
    },
    currentHours() {
      return this.date().getHours();
    },
    currentMinutes() {
      return "0" + this.date().getMinutes();
    },
    currentSeconds() {
      return "0" + this.date().getSeconds();
    },
    timestampToHour() {
      const formattedTime = `${this.currentHours()}:${this.currentMinutes().substr(
        -2
      )}:${this.currentSeconds().substr(-2)}`;
      //  const timeToHour = function () {
      // (this.hours * 1000).getHours();
      // }
      // console.log(() => (this.timestamp * 1000).getHours());

      // console.log((this.currentHours()));
      // console.log((this.currentMinutes()));
      // console.log((this.currentSeconds()));
      // console.log(formattedTime);
      this.formatted = formattedTime;
      // return (this.timestamp * 1000).getHours();
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="css" scoped src="../../node_modules/bootstrap/dist/css/bootstrap.css">
</style>
