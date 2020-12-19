<template>
  <q-page class="flex flex-center">
    <video
      ref="video"
      class="video-js vjs-default-button vjs-big-play-centered"
      controls
      playsinline
      preload="auto"
      width="640"
      height="480"
      data-setup="{}"
    >
      <source :src="url" type="application/x-mpegURL" />
      <p class="vjs-no-js">
        To view this video please enable JavaScript, and consider upgrading to a
        web browser that
        <a href="https://videojs.com/html5-video-support/" target="_blank"
          >supports HTML5 video</a
        >
      </p>
    </video>
  </q-page>
</template>

<script>
import videojs from "video.js";

import "videojs-contrib-quality-levels";
import "videojs-hls-quality-selector";

export default {
  name: "PageIndex",
  data() {
    return {
      url: "http://localhost:80/vod/sample.mp4/index.m3u8",
    };
  },
  mounted() {
    const options = {
      sources: [
        {
          src: this.url,
          type: "application/x-mpegURL",
        },
      ],
      // 'poster' : this.urlPoster
    };

    this.player = videojs(this.$refs.video, options, function onPlayerReady() {
      console.log("Player ready");
      var myPlayer = this;

      myPlayer.hlsQualitySelector({
        displayCurrentQuality: true,
      });
    });
  },
  destroyed() {
    if (this.player != null) {
      this.player.dispose();
    }
  },
};
</script>
