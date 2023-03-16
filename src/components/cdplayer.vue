<template>
  <div>
    <select v-model="currentSong">
      <option v-for="song in songlist" :value="song">{{ song }}</option>
    </select>
    <button @click="playerPause">{{ isPlaying ? "Pauce" : "Play" }}</button>
    <button @click="stop">Stop</button>
    <button @click="skip">Skip</button>
  </div>
</template>
<script setup>
import { ref } from "vue";
const songList = ref(["Song A", "Song B", "Song C"]);
const currentSong = ref(songList.value[0]);
const isPlaying = ref(false);

const playerPause = () => {
  isPlaying.value = !isPlaying.value;
};
const skip = () => {
  const currentIndex = songList.value.indexOf(currentSong.value);
  if (currentIndex === songList.value.length - 1) {
    currentSong.value = songlist.value[0];
  } else {
    currentSong.value = songList.value[currentIndex + 1];
  }
  isPlaying.value = true;
};
</script>

<style scoped></style>
