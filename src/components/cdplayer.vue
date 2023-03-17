<template>
  <div class="music-player">
    <h2>{{ currentSong.title }}</h2>
    <h4>{{ currentSong.artist }}</h4>
    <img :src="currentSong.albumCover" :alt="currentSong.alt" />
    <div class="controls">
      <button @click="togglePlay">{{ isPlaying ? "暂停" : "播放" }}</button>
      <button @click="stop">停止</button>
      <button @click="skip">下一曲</button>
    </div>
  </div>
</template>
<script setup>
import { ref, watch } from "vue";
const songList = ref([
  {
    title: "BurgerKing",
    artist: "How2Bboss",
    url: "/src/assets/BurgerKing.mp3",
    albumCover: "/src/assets/BurgerKing.png",
    alt: "makima.png",
  },
  {
    title: "Song 2",
    artist: "JSON02",
    url: "../assets/suchmos.mp3",
    albumCover: "@/assets/makima.png",
    alt: "makima.png",
  },
  {
    title: "Song 3",
    artist: "JSON03",
    url: "song3.mp3",
    albumCover: "../assets/album3.png",
  },
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
  audio.onloadeddata = () => {
    if (isPlaying.value) {
      audio.play();
    }
  };
};

loadSong();

const play = () => {
  audio.play();
};
const pause = () => {
  audio.pause();
};

loadSong();
</script>

<style scoped></style>
