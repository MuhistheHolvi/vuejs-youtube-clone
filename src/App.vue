<template>
  <div class="container">
    <search-bar @termChange="onTermChange"></search-bar>
    <video-list
      v-if="searchResults.length > 0"
      :videos="searchResults"
    ></video-list>
    <div v-if="error.length">{{ error }}</div>
  </div>
</template>

<script>
import axios from "axios";
import searchBar from "./components/searchBar";
import VideoList from "./components/videoList";
const API_KEY = "AIzaSyBp75kKYtNjJINRh--Xy2D3jqtzDlMS_Ew";
export default {
  components: { searchBar, VideoList },
  name: "App",
  data: () => {
    return { searchResults: [], renderResults: false, error: {} };
  },
  methods: {
    onTermChange(searchTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            q: searchTerm,
          },
        })
        .then((response) => {
          if (response.data) {
            this.updateVideoList(response);
          }
        })
        .catch(function (error) {
          console.log(error.response);
        });
    },
    updateVideoList(response) {
      if (response.data?.items) {
        this.searchResults = response.data.items;
      }
    },
  },
};
</script>