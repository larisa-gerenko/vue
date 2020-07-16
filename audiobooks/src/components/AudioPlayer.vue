<template>
  <div>
    <div class="image"></div>
    <div class="player-wrapper">
      <div class="player">
        <div class="player-controls">
          <button class="back" v-on:click="prevTrack" title="Backward">
            <i class="fa fa-step-backward" aria-hidden="true"></i>
          </button>

          <button class="play" v-on:click="play" title="Play/Pause">
            <i class="fa fa-play" aria-hidden="true"></i>
          </button>

          <button class="stop" v-on:click="stop" title="Stop">
            <i class="fa fa-stop" aria-hidden="true"></i>
          </button>

          <button class="forward" v-on:click="nextTrack" title="Forward">
            <i class="fa fa-step-forward" aria-hidden="true"></i>
          </button>
        </div>
      </div>
    </div>
    <div class="list">
      <div
        v-for="(track, index) in audiotracks"
        v-bind:key="track.name"
        v-on:click="playTrack(track.src, index)"
      >{{track.name}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "audio-player",
  data: function() {
    const audio = new Audio();
    return {
      currentTrack: audio,
      currentIndex: 0
    };
  },
  props: ["audiotracks"],
  methods: {
    play() {
      this.currentTrack.play();
    },
    stop() {
      this.currentTrack.pause();
      this.currentTrack.currentTime = 0;
    },
    playTrack(src, index) {
      this.currentTrack.currentTime = 0;
      this.currentTrack.src = src;
      this.currentTrack.play();
      this.currentIndex = index;
    },
    nextTrack() {
      const nextIndex = this.currentIndex + 1;
      if (nextIndex >= this.audiotracks.length) {
        return;
      }
      const nextTrack = this.audiotracks[nextIndex];
      this.playTrack(nextTrack.src, nextIndex);
    },
    prevTrack() {
      const prevIndex = this.currentIndex - 1;
      if (prevIndex < 0) {
        return;
      }
      const prevTrack = this.audiotracks[prevIndex];
      this.playTrack(prevTrack.src, prevIndex);
    }
  }
};
</script>

<style scoped>
/* .image {
    background-image: url(./src/assets/logo.jpg);
 }
 */

.player-wrapper {
  align-items: center;
  background-color: #fff;
  display: flex;
  justify-content: center;
}

.player-controls {
  display: flex;
}

button {
  margin-right: 30px;
  color: black;
  background: none;
  border: none;
  font-size: 20px;
}

.play {
  color: #6e6 !important;
  font-size: 30px;
}
</style>
