<template>
  <div class="container">
    <search-bar @termChange="onTermChange"></search-bar>
    <video-item :video="selectedVideo"></video-item>
    <video-list
      v-if="searchResults.length > 0"
      :videos="searchResults"
      @videoSelect="onVideoSelect"
    ></video-list>
  </div>
</template>

<script>
import axios from "axios";
import searchBar from "./components/searchBar";
import VideoList from "./components/videoList";
import videoItem from "./components/videoItem";
const API_KEY = "AIzaSyBp75kKYtNjJINRh--Xy2D3jqtzDlMS_Ew";
export default {
  components: { searchBar, VideoList, videoItem },
  name: "App",
  data: () => {
    return {
      searchResults: [],
      selectedVideo: null,
    };
  },
  methods: {
    onVideoSelect(video) {
      this.selectedVideo = video;
    },
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
          this.updateVideoList(response);
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