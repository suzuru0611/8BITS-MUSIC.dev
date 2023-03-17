<template>
  <div>
    <h1>{{ currentSong.title }}</h1>
    <h1>{{ currentSong.artist }}</h1>
    <button @click="togglePlay">{{ isPlaying ? "Pauce" : "Play" }}</button>
    <button class="p-5" @click="stop">Stop</button>
    <button @click="skip">Skip</button>
  </div>
</template>
<script setup>
import { ref, watch } from "vue";
const songList = ref([
  { title: "Song 1", artist: "JSON01", url: "song1.mp3" },
  { title: "Song 2", artist: "JSON02", url: "song2.mp3" },
  { title: "Song 3", artist: "JSON03", url: "song3.mp3" },
]);
const currentSong = ref(songList.value[0]);
const isPlaying = ref(false);

const audio = new Audio();
const togglePlay = () => {
  if (isPlaying.value) {
    audio.pause();
  } else {
    audio.play();
  }
  isPlaying.value = !isPlaying.value;
};

const stop = () => {
  audio.pause();
  audio.currentTime = 0;
  isPlaying.value = false;
};

const skip = () => {
  const currentIndex = songList.value.indexOf(currentSong.value);
  if (currentIndex === songList.value.length - 1) {
    currentSong.value = songList.value[0];
  } else {
    currentSong.value = songList.value[currentIndex + 1];
  }
  isPlaying.value = true;
  loadSong();
};

const loadSong = () => {
  audio.src = currentSong.value.url;
  audio.load();
  if (isPlaying.value) {
    audio.play();
  }
};

loadSong();

const play = () => {
  audio.play;
};
const pause = () => {
  audio.pause;
};

loadSong();
</script>

<style scoped></style>
