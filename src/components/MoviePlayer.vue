<template>
  <video ref="videoPlayer" @loadedmetadata="loadData" @timeupdate="timeLogger" controls>
    <source :src="movie.filePath" type="video/mp4">
  </video>
</template>

<script>
import {ref} from "vue";

export default {
  name: "MoviePlayer",
  props: ['movie'],
  setup() {
    const videoPlayer = ref(null);
    const duration = ref(0);
    const halfDuration = ref(0);
    const lastEventTime = ref(0);

    function timeLogger() {
      if ((Date.now() - lastEventTime.value) >= 1000) {
        lastEventTime.value = Date.now();

        const currentTime = Math.floor(videoPlayer.value.currentTime);
        if (currentTime === 0) {
          console.log("Początek");
        }
        if (halfDuration.value == currentTime) {
          console.log("Polowa")
        }
        if (currentTime == duration.value) {
          console.log("Koniec");
        }
      }
    }
    function loadData() {
      this.duration = Math.floor(videoPlayer.value.duration);
      this.halfDuration = Math.floor(videoPlayer.value.duration / 2);
    }
    return {videoPlayer, duration, halfDuration, loadData, timeLogger, lastEventTime}
  }
}
</script>

<style scoped>
</style>