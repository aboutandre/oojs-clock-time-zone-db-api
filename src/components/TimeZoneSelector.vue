<template>
  <div>
    <v-select label="zoneName" :options="zoneNames"/>
  </div>
</template>
<script>
import axios from "axios";
import vSelect from "../../node_modules/vue-select/src/components/Select.vue";

export default {
  data() {
    return {
      zoneList: null,
      zoneNames: []
    };
  },
  components: {
    vSelect
  },
  watch: {
    zoneList: function() {
      this.sortCities();
    }
  },
  mounted() {
    axios
      .get(
        "http://api.timezonedb.com/v2.1/list-time-zone?key=PVVEZXX7L9E5&format=json"
      )
      .then(response => (this.zoneList = response.data.zones));
  },
  methods: {
    sortCities() {
      this.zoneNames = this.zoneList.slice();
      this.zoneNames.sort(function(a, b) {
        if (a.zoneName < b.zoneName) {
          return -1;
        } else if (a.zoneName > b.zoneName) {
          return 1;
        }
        return 0;
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
