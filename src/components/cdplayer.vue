<template>
  <div
    class="flex h-screen w-screen items-center justify-center overflow-hidden bg-yellow-500"
  >
    <div class="flex w-full flex-col justify-center pt-5 pb-5">
      <div>
        <p class="nes-balloon from-left nes-pointer">
          This is suzuru's 8-Bits space, the music part is made by How2Bboss and
          me, we are a group of people who use Famistudio to make Nintendo-like
          music
          <i class="nes-jp-logo"></i>
          <i class="snes-jp-logo"></i>
          <i class="snes-logo"></i>
        </p>
        <section class="message-list">
          <section class="message -left flex flex-row">
            <i class="nes-bcrikko"></i>
            <!-- Balloon -->
            <div class="nes-balloon from-left">
              <p>Click The Play Button!!</p>
            </div>
          </section>

          <section class="message -right flex flex-row">
            <!-- Balloon -->
            <div class="nes-balloon from-right">
              <p>Hmmmm....Tight,Tight,Tight...Yeah!!!</p>
            </div>
            <i class="nes-bcrikko"></i>
          </section>
          <section class="message -right flex flex-row">
            <!-- Balloon -->
            <div class="nes-balloon from-right">
              <p>
                Mario,MegaMen,Sonic! Whatever Man, Just Keep Bringing Me That!
              </p>
            </div>
            <i class="nes-bcrikko"></i>
          </section>
        </section>
      </div>
      <section class="icon-list">
        <!-- phone -->
        <i class="nes-smartphone"></i>
      </section>
    </div>
    <div class="align-center flex flex-col">
      <div class="flex w-full justify-center">
        <section class="nes-container with-title w-4/6">
          <h2 class="title">{{ currentSong.artist }}</h2>
          <p>{{ currentSong.title }}</p>
        </section>
      </div>
      <div class="flex flex-col items-center pt-3 pb-3">
        <div class="w-4/6" :class="{ 'is-playing': isPlaying }">
          <img :src="currentSong.albumCover" :alt="currentSong.alt" />
        </div>
      </div>
      <div class="flex w-full flex-row justify-center">
        <button class="pr-2 pl-2" @click="previous">
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
        <button class="pr-2 pl-2" @click="togglePlay">
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
        <button class="pr-2 pl-2" @click="next">
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
.nes-container.with-title > .title {
  display: table;
  padding: 0 0.5rem;
  margin: -1.8rem 0 1rem;
  font-size: 1rem;
  background-color: rgb(234 179 8 / var(--tw-bg-opacity));
}

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
