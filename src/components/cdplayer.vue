<template>
  <div
    class="flex h-screen w-screen flex-col justify-center overflow-hidden bg-yellow-500"
  >
    <div class="flex flex-col items-center">
      <p class="font-sans text-4xl font-bold">{{ currentSong.title }}</p>
      <p class="pt-3 text-2xl">{{ currentSong.artist }}</p>
    </div>
    <div class="flex w-full justify-center pt-5 pb-5">
      <div class="w-4/6 lg:w-2/6">
        <div class="album-cover" :class="{ 'is-playing': isPlaying }">
          <img :src="currentSong.albumCover" :alt="currentSong.alt" />
        </div>
      </div>
    </div>
    <div class="flex w-full flex-row justify-center">
      <button @click="previous">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="#d0021b"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <polygon points="11 19 2 12 11 5 11 19"></polygon>
          <polygon points="22 19 13 12 22 5 22 19"></polygon>
        </svg>
      </button>
      <button class="pr-5 pl-5" @click="togglePlay">
        <svg
          v-if="isPlaying"
          xmlns="http://www.w3.org/2000/svg"
          width="33"
          height="33"
          viewBox="0 0 24 24"
          fill="none"
          stroke="#d0021b"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <rect x="6" y="4" width="4" height="16"></rect>
          <rect x="14" y="4" width="4" height="16"></rect>
        </svg>
        <svg
          v-else
          xmlns="http://www.w3.org/2000/svg"
          width="33"
          height="33"
          viewBox="0 0 24 24"
          fill="none"
          stroke="#d0021b"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <polygon points="5 3 19 12 5 21 5 3"></polygon>
        </svg>
      </button>
      <button @click="next">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="#d0021b"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <polygon points="13 19 22 12 13 5 13 19"></polygon>
          <polygon points="2 19 11 12 2 5 2 19"></polygon>
        </svg>
      </button>
    </div>
  </div>
</template>
<script setup>
import { ref, watch, computed } from "vue";
const songList = ref([
  {
    title: "City-original",
    artist: "How2Bboss",
    url: "/src/assets/City.mp3",
    albumCover: "/src/assets/City.png",
    alt: "City.png",
  },
  {
    title: "BurgerKing-remix",
    artist: "How2Bboss",
    url: "/src/assets/BurgerKing.mp3",
    albumCover: "/src/assets/BurgerKing.png",
    alt: "BurgerKing.png",
  },
  {
    title: "Mario-remix",
    artist: "How2Bboss",
    url: "/src/assets/Mario.mp3",
    albumCover: "/src/assets/Mario.png",
    alt: "Mario.png",
  },
  {
    title: "Sonic-remix",
    artist: "How2Bboss",
    url: "/src/assets/Sonic.mp3",
    albumCover: "/src/assets/Sonic.png",
    alt: "Sonic.png",
  },
  {
    title: "MegaMen-remix",
    artist: "How2Bboss",
    url: "/src/assets/MegaMen.mp3",
    albumCover: "/src/assets/MegaMen.png",
    alt: "MegaMen.png",
  },
  {
    title: "Toasty-original",
    artist: "How2Bboss",
    url: "/src/assets/Toasty.mp3",
    albumCover: "/src/assets/Toasty.png",
    alt: "Toasty.png",
  },
  {
    title: "Splatoon-remix",
    artist: "SUZURU",
    url: "/src/assets/Splatoon.mp3",
    albumCover: "/src/assets/Splatoon.png",
    alt: "Splatoon.png",
  },
  {
    title: "Village-original",
    artist: "How2Bboss",
    url: "/src/assets/Village.mp3",
    albumCover: "/src/assets/Village.png",
    alt: "Village.png",
  },
  {
    title: "Rydeen-remix",
    artist: "SUZURU",
    url: "/src/assets/Rydeen.mp3",
    albumCover: "/src/assets/Rydeen.png",
    alt: "Rydeen.png",
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

const next = () => {
  const currentIndex = songList.value.indexOf(currentSong.value);
  if (currentIndex === songList.value.length - 1) {
    currentSong.value = songList.value[0];
  } else {
    currentSong.value = songList.value[currentIndex + 1];
  }
  isPlaying.value = true;
  loadSong();
};

const previous = () => {
  const currentIndex = songList.value.indexOf(currentSong.value);
  if (currentIndex === 0) {
    currentSong.value = songList.value[8];
  } else {
    currentSong.value = songList.value[currentIndex - 1];
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

const play = () => {
  audio.play();
};
const pause = () => {
  audio.pause();
};

watch(isPlaying, (newVal) => {
  const albumCover = document.querySelector(".album-cover");
  if (newVal) {
    albumCover.classList.add("is-playing");
  } else {
    albumCover.classList.remove("is-playing");
  }
});

loadSong();
</script>

<style scoped>
.album-cover {
  display: inline-block;
  position: relative;
}

.album-cover.is-playing img {
  animation: spin 2s linear infinite;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
