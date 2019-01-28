<template>
  <div class="p-3">
    <span>{{ locationData }}</span>
    <div class="d-flex flex-column pt-3">
      <button class="btn btn-primary mb-3" @click="unixTime()">Show me the time</button>
      <button class="btn btn-secondary mb-3" @click="timestampToHour()">Show me the hours</button>
      <span>This is formatted: {{ formatted }}</span>
      <span>This is lng: {{ lng }}</span>
      <span>This is lat: {{ lat }}</span>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      locationData: null,
      info: null,
      timestamp: null,
      hours: null,
      dst: null,
      formatted: null,
      lng: null,
      lat: null
    };
  },
  watch: {
    locationData: function() {
      this.timestamp = this.locationData.timestamp;
      this.dstCheck();
      this.timestampToHour();

      console.log(
        "This is the longitude: " +
          this.lng +
          ". This is the latitude: " +
          this.lat
      );
    }
  },
  mounted() {
    axios
      .get(
        "http://api.ipstack.com/217.110.78.178?access_key=80a79bb513023e29f6d21c4785a67ef8"
      )
      .then(
        response => (
          this.lng = response.data.longitude,
          this.lat = response.data.latitude,
          axios
            .get(
              "http://api.timezonedb.com/v2.1/get-time-zone?key=PVVEZXX7L9E5&format=json&by=position&lat=" +
                this.lat +
                "&lng=" +
                this.lng
            )
            .then(response => (this.locationData = response.data))
        )
      );
  },
  methods: {
    dstCheck() {
      return (this.dst = this.locationData.dst);
    },
    unixTime() {
      console.log(this.timestamp);
      console.log(this.info);
    },
    date() {
      const thisTimeStamp = new Date(this.timestamp * 1000);
      return thisTimeStamp;
    },
    currentHours() {
      if (this.dst === "0") {
        return this.date().getHours() - 1;
      } else {
        return this.date().getHours();
      }
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
      this.formatted = formattedTime;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="css" scoped src="../../node_modules/bootstrap/dist/css/bootstrap.css">
</style>
