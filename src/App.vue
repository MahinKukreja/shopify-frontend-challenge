<template>
  <div>
    <br />
    <!-- Make an API component for each day in daysAgo -->
    <div :key="day" v-for="day in daysAgo">
      <API :apiDate="day" />
    </div>
  </div>
</template>

<script>
import moment from "moment";
import API from "./components/API.vue";
export default {
  name: "App",
  components: {
    API,
  },
  data() {
    return {
      // Empty array for holding days
      daysAgo: [],
    };
  },
  created() {
    // Get the properly formatted date for the past 7 days
    for (var i = 0; i < 7; i++) {
      this.daysAgo[i] = moment().subtract(i, "days").format("Y-MM-DD");
    }
  },
};
</script>

<style>
* {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  text-align: center;
  color: whitesmoke;
  background-color: #080808;
}
</style>
