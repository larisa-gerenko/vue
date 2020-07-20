<template>
  <div id="app">
    <div class="box-center">
      <audio-player
        :audiotracks="[
          {name: 'Summer', src: 'https://www.bensound.com/bensound-music/bensound-summer.mp3', time: '2:43'},
        {name: 'Ukulele', src: 'https://www.bensound.com/bensound-music/bensound-ukulele.mp3', time: '2:43'},
        {name: 'Creative Minds', src: 'https://www.bensound.com/bensound-music/bensound-creativeminds.mp3', time: '2:43'},
        {name: 'A New Beginning', src: 'https://www.bensound.com/bensound-music/bensound-anewbeginning.mp3', time: '2:43'},
        {name: 'Little Idea', src: 'https://www.bensound.com/bensound-music/bensound-littleidea.mp3', time: '2:43'}]"
      ></audio-player>
    </div>
  </div>
</template>

<script>
import AudioPlayer from "./components/AudioPlayer.vue";

export default {
  name: "App",
  components: {
    AudioPlayer
  }
};
</script>

<style>
@import url("https://use.fontawesome.com/releases/v5.0.13/css/all.css");
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,400;0,500;1,400&display=swap");

#app {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
.box-center {
  width: 500px;
  box-shadow: 0 0 45px -8px #c1c1c1;
  border-radius: 5px;
  border: 1px solid #efefef;
}
</style>
