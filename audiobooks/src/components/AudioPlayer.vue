<template>
  <div class="audioplayer">
    <div class="image">
      <img src="@/assets/logo.jpg" alt />
    </div>
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
        <div class="volume">
          <input type="range" v-on:change="changeVolume" min="0" max="1" value="1" step="0.1" />
        </div>
      </div>
    </div>

    <div class="list">
      <div
        class="track"
        v-for="(track, index) in audiotracks"
        v-bind:key="track.name"
        v-on:click="playTrack(track.src, index)"
      >
        <span>{{track.name}}</span>
        <span>{{track.time}}</span>
      </div>
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
  mounted() {
    const track = this.audiotracks[this.currentIndex];
    this.currentTrack.src = track.src;
    this.currentTrack.onended = () => {
      this.nextTrack();
    };
  },
  methods: {
    play() {
      this.currentTrack.play();
    },
    stop() {
      this.currentTrack.pause();
      this.currentTrack.currentTime = 0;
    },
    playTrack(src, index) {
      this.currentTrack.src = src;
      this.currentTrack.play();
      this.currentIndex = index;
      this.currentTrack.onended = () => {
        this.nextTrack();
      };
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
    },
    changeVolume(ev) {
      this.currentTrack.volume = ev.target.value;
    }
  }
};
</script>

<style scoped>
.audioplayer {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.image {
  height: 200px;
}
.player-wrapper {
  align-items: center;
  background-color: #fff;
  display: flex;
  flex-grow: 1;
  justify-content: center;
}
.volume {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}
.player-controls {
  display: flex;
}

button {
  margin: 0 15px;
  color: black;
  background: none;
  border: none;
  font-size: 20px;
}

.play {
  color: #6e6 !important;
  font-size: 30px;
}
.list {
  box-shadow: inset 0 6px 16px -12px #c1c1c1;
  height: auto;
  width: 500px;
  border: 1px solid #eee;
}
.track {
  display: flex;
  justify-content: space-between;
  margin-left: 5px;
  color: #666;
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  padding: 5px;
  border-bottom: 1px solid #eee;
  line-height: 2;
}
</style>
