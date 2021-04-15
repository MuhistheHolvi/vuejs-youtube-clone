<template>
  <div>
    <ul class="list-group col-md-4">
      <video-list-item
        v-for="(video, index) in videos"
        :key="index"
        :searchResultItem="video"
        @videoSelect="onVideoSelect"
      ></video-list-item>
    </ul>
  </div>
</template>

<script>
import videoListItem from "./videoListItem.vue";

export default {
  components: { videoListItem },
  name: "VideoList",
  props: {
    videos: Array,
  },
  methods: {
    onVideoSelect(video) {
      this.$emit("videoSelect", video);
    },
  },
};
</script>

<style>
</style>