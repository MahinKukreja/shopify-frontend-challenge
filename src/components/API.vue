<template>
  <div>
    <!-- Title, Image, Explanation, Like Button and a Divider -->
    <h1>
      <u>{{ title }}</u>
    </h1>
    <b-img v-bind:src="url" rounded thumbnail fluid alt="APOD NASA" />
    <h4>{{ date }}'s Astronomy Picture of the Day</h4>
    <p>{{ snippet }}</p>
    <div class="cursor">
      <LikeButton />
    </div>
    <br />
    <hr style="width: 80%; margin: auto" />
    <br />
  </div>
</template>

<script>
// For API Requests
import axios from "axios";
// For Date Formatting
import moment from "moment";
import LikeButton from "./LikeButton.vue";

export default {
  name: "API",
  components: {
    LikeButton,
  },
  props: {
    apiDate: {
      type: String,
      // Default to current date if none provided
      default: function () {
        return moment(new Date()).format("Y-MM-DD");
      },
    },
  },
  data() {
    // Initialize Data
    return {
      url: null,
      snippet: null,
      title: null,
      date: null,
    };
  },
  created() {
    // Fill Data from API request
    let url = `https://api.nasa.gov/planetary/apod?api_key=PBCplJHkkhw0WCvgAhdJnXCrVMlAlg5ZQ5WnngiH&date=${this.apiDate}`;
    axios.get(url).then((res) => {
      this.url = res.data.hdurl;
      this.snippet = res.data.explanation;
      this.title = res.data.title;
      this.date = moment(res.data.date, "Y-M-D").format("MMMM D, Y"); // Includes Date Formatting
    });
  },
};
</script>

<style>
p {
  margin-left: auto;
  margin-right: auto;
  width: 100%;
  max-width: 1000px;
}

h4 {
  padding-top: 10px;
  margin-top: 10px;
}

.cursor {
  cursor: pointer;
}

hr {
  width: 80%;
  align-content: center;
  text-align: center;
}
</style>