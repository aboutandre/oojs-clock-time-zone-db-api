<template>
  <div class="p-3 flex-grow-1 d-flex flex-column justify-content-center">
    <div class="d-flex flex-column">
      <h1>Based on your current location your time is:</h1>
      <div class="time">
        <h2 class="formatted-time">{{ formatted }}</h2>
      </div>
    </div>
    <div class="pt-5">
      <h4 class="pb-3">Here are some photos taken near you:</h4>
      <img :src="imageURL" alt class="background-image">
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
      lat: null,
      imagesFound: null,
      imageSelected: null,
      imageTitle: null,
      backgroundImage: null,
      farmNumber: null,
      serverId: null,
      imageId: null,
      imageSecret: null,
      imageURL: null
    };
  },
  watch: {
    locationData: function() {
      this.startApp();
    },
    timestamp: function() {
      this.timestampToHour();
    }
  },
  mounted() {
    axios
      .get(
        "http://api.ipstack.com/217.110.78.178?access_key=80a79bb513023e29f6d21c4785a67ef8"
      )
      .then(
        response => (
          (this.lng = response.data.longitude),
          (this.lat = response.data.latitude),
          axios
            .get(
              "http://api.timezonedb.com/v2.1/get-time-zone?key=PVVEZXX7L9E5&format=json&by=position&lat=" +
                this.lat +
                "&lng=" +
                this.lng
            )
            .then(
              response => (
                (this.locationData = response.data),
                axios
                  .get(
                    "https://api.flickr.com/services/rest/?method=flickr.photos.search" +
                      "&api_key=0b270aa1f49e1401b78e7854c537189c" +
                      "&lat=" +
                      this.lat +
                      "&lon=" +
                      this.lng +
                      "&format=json&nojsoncallback=1"
                  )

                  .then(
                    response => (
                      (this.imagesFound = response.data.photos.photo.length),
                      this.getRandomImage(),
                      (this.backgroundImage = response.data.photos.photo[this.imageSelected]),
                      (this.farmNumber = this.backgroundImage.farm),
                      (this.serverId = this.backgroundImage.server),
                      (this.imageId = this.backgroundImage.id),
                      (this.imageSecret = this.backgroundImage.secret),
                      (this.imageTitle = this.backgroundImage.title),
                      this.setBackgroundImage()
                    )
                  )
              )
            )
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
    },
    runClock() {
      const updateClock = function() {
        this.timestamp = this.timestamp + 1;
      };
      setInterval(updateClock.bind(this), 1000);
    },
    getRandomImage() {
      this.imageSelected = Math.floor(
        Math.random() * Math.floor(this.imagesFound)
      );
    },
    setBackgroundImage() {
      this.imageURL = `https://farm${this.farmNumber}.staticflickr.com/${this.serverId}/${this.imageId}_${this.imageSecret}.jpg`;
    },
    startApp() {
      this.timestamp = this.locationData.timestamp;
      this.dstCheck();
      this.runClock();
      this.timestampToHour();
      this.setBackgroundImage();

      console.log(
        "This is the longitude: " +
          this.lng +
          ". This is the latitude: " +
          this.lat +
          ". This is the timestamp: " +
          this.timestamp +
          ". This image data: " +
          this.backgroundImage
      );
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.background-image {
  border: 1em solid #fcfcfc;
  border-radius: 1.5em;
  width: 100%;
  height: auto;
  transform: rotate3d(0, 0, 1, -1.2deg);
}

h1,
h2,
h3 {
  font-weight: 300;
}
</style>
