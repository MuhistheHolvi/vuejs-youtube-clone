<template>
  <div>
    <li class="list-group-item media">
      <img class="mr-3" :src="imageUrl" alt="snippet.description" />
      <div class="media-body">
        {{ videoTitle }}
      </div>
    </li>
  </div>
</template>

<script>
export default {
  title: "videoList",
  props: {
    searchResultItem: Object,
  },
  computed: {
    videoTitle() {
      return this.snippet.title;
    },
    imageUrl() {
      return this.snippet.thumbnails?.default?.url;
    },
    imageHeight() {
      return this.snippet.thumbnails?.default?.height;
    },
    imageWidth() {
      return this.snippet.thumbnails?.default?.width;
    },
    videolUrl() {
      const videoId = this.searchResultItem?.id.videoId;
      return `https://www.youtube.com/watch?v=${videoId}`;
    },
    snippet() {
      return this.searchResultItem?.snippet;
    },
  },
};
</script>

<style scoped>
li {
  display: flex;
  cursor: pointer;
}
li:hover {
  background-color: #eee;
}
</style>