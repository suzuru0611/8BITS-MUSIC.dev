<template>
  <div class="items-center bg-yellow-500">
    <main class="flex min-h-[110vh] items-center py-[8rem] leading-loose tracking-wide xl:min-h-[100vh]">
      <section class="hidden w-4/6 flex-col 2xl:flex">
        <div class="ml-[10rem] flex flex-col">
          <div class="py-5">
            <h4>
              -------------
              <i class="snes-jp-logo"></i>
              -------------
            </h4>
            <P> Here is the 8BITS music library </P>
          </div>
          <div>
            <h4>
              <i class="nes-icon trophy"></i>
              WHY?
            </h4>
            <P>
              We will start to make 8BIT music, mainly because we like Nintendo
              games, so we start to create related music, and finally want to
              store your works in an interesting way, here are not only
              Nintendo-related creations, but also other types of 8BITS Music
              adaptation, hope you like it.
            </P>
          </div>
          <div class="py-5">
            <h4>
              <i class="nes-icon star"></i>
              MEMBER
            </h4>
            <P>
              Most of the music here is provided by How2Bboss, I am responsible
              for a small part of the music and the rest of the programming and
              so on, this website would not be possible without him, thank you
              very much for his selfless help.
            </P>
            <div class="pd-4 flex flex-nowrap pt-5">
              <section class="nes-container is-dark member-card flex">
                <img class="inline-block h-12 w-12 rounded-full ring-2 ring-white" src="/src/assets/suzuru_icon.jpg"
                  alt="" />
                <div class="ml-3 mr-2 flex w-40 flex-col">
                  <h4>suzuru</h4>
                  <p class="text-[10px]">web,ill,music</p>
                </div>
              </section>
              <section class="nes-container is-dark member-card flex">
                <img class="inline-block h-12 w-12 rounded-full ring-2 ring-white" src="/src/assets/boss_icon.jpg"
                  alt="" />
                <div class="ml-3 mr-2 flex w-40 flex-col">
                  <h4>How2Bboss</h4>
                  <p class="text-[10px]">music</p>
                </div>
              </section>
            </div>
          </div>
          <div class="py-5">
            <h4>
              <i class="nes-icon coin"></i>
              MORE...
            </h4>
            <P> Other works by SUZURU </P>
            <section class="flex flex-row">
              <a href="https://suzuru0611.github.io/SUZURU/">
                <div>SUZURU MAIN WEBSITE</div>
              </a>
            </section>
            --------------------------------
          </div>
        </div>
      </section>
      <section class="w-full flex-col items-center md:p-0">
        <div class="flex w-full flex-col items-center">
          <section class="nes-container with-title w-4/6 md:w-3/6">
            <h2 class="title">{{ currentSong.artist }}</h2>
            <p>{{ currentSong.title }}</p>
          </section>
        </div>
        <div class="flex w-full justify-center pt-5 pb-5">
          <div class="w-5/6 md:w-3/6">
            <div class="album-cover" :class="{ 'is-playing': isPlaying }">
              <img :src="currentSong.albumCover" :alt="currentSong.alt" />
            </div>
          </div>
        </div>
        <div class="flex w-full flex-row justify-center">
          <button class="mx-2 px-1" @click="previous">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
              stroke="#d0021b" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <polygon points="11 19 2 12 11 5 11 19"></polygon>
              <polygon points="22 19 13 12 22 5 22 19"></polygon>
            </svg>
          </button>
          <button class="mx-2 px-1" @click="togglePlay">
            <svg v-if="isPlaying" xmlns="http://www.w3.org/2000/svg" width="33" height="33" viewBox="0 0 24 24"
              fill="none" stroke="#d0021b" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <rect x="6" y="4" width="4" height="16"></rect>
              <rect x="14" y="4" width="4" height="16"></rect>
            </svg>
            <svg v-else xmlns="http://www.w3.org/2000/svg" width="33" height="33" viewBox="0 0 24 24" fill="none"
              stroke="#d0021b" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <polygon points="5 3 19 12 5 21 5 3"></polygon>
            </svg>
          </button>
          <button class="mx-2 px-1" @click="next">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
              stroke="#d0021b" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <polygon points="13 19 22 12 13 5 13 19"></polygon>
              <polygon points="2 19 11 12 2 5 2 19"></polygon>
            </svg>
          </button>
        </div>
      </section>
    </main>
    <notice class="flex bg-yellow-500 pl-[2rem] pb-[2rem] 2xl:hidden">
      <p class="text-[10px] text-yellow-100">
        Music Copyright © NINTENDO,YMO. All Rights Reserved.
      </p>
    </notice>
  </div>
</template>
<script setup>
import { ref, watch } from "vue";
import city_png from "/src/assets/City.png";
import city_mp3 from "/src/assets/City.mp3";
import burgerKing_png from "/src/assets/BurgerKing.png";
import burgerKing_mp3 from "/src/assets/BurgerKing.mp3";
import Mario_png from "/src/assets/Mario.png";
import Mario_mp3 from "/src/assets/Mario.mp3";
import Sonic_png from "/src/assets/Sonic.png";
import Sonic_mp3 from "/src/assets/Sonic.mp3";
import MegaMen_png from "/src/assets/MegaMen.png";
import MegaMen_mp3 from "/src/assets/MegaMen.mp3";
import Toasty_png from "/src/assets/Toasty.png";
import Toasty_mp3 from "/src/assets/Toasty.mp3";
import Splatoon_png from "/src/assets/Splatoon.png";
import Splatoon_mp3 from "/src/assets/Splatoon.mp3";
import Village_png from "/src/assets/Village.png";
import Village_mp3 from "/src/assets/Village.mp3";
import Rydeen_png from "/src/assets/Rydeen.png";
import Rydeen_mp3 from "/src/assets/Rydeen.mp3";

const songList = ref([
  {
    title: "City-original",
    artist: "How2Bboss",
    url: city_mp3,
    albumCover: city_png,
    alt: "City.png",
  },
  {
    title: "BurgerKing-remix",
    artist: "How2Bboss",
    url: burgerKing_mp3,
    albumCover: burgerKing_png,
    alt: "BurgerKing.png",
  },
  {
    title: "Mario-remix",
    artist: "How2Bboss",
    url: Mario_mp3,
    albumCover: Mario_png,
    alt: "Mario.png",
  },
  {
    title: "Sonic-remix",
    artist: "How2Bboss",
    url: Sonic_mp3,
    albumCover: Sonic_png,
    alt: "Sonic.png",
  },
  {
    title: "MegaMen-remix",
    artist: "How2Bboss",
    url: MegaMen_mp3,
    albumCover: MegaMen_png,
    alt: "MegaMen.png",
  },
  {
    title: "Toasty-original",
    artist: "How2Bboss",
    url: Toasty_mp3,
    albumCover: Toasty_png,
    alt: "Toasty.png",
  },
  {
    title: "Splatoon-remix",
    artist: "SUZURU",
    url: Splatoon_mp3,
    albumCover: Splatoon_png,
    alt: "Splatoon.png",
  },
  {
    title: "Village-original",
    artist: "How2Bboss",
    url: Village_mp3,
    albumCover: Village_png,
    alt: "Village.png",
  },
  {
    title: "Rydeen-remix",
    artist: "SUZURU",
    url: Rydeen_mp3,
    albumCover: Rydeen_png,
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
.nes-container.with-title>.title {
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
  animation: spin 3s linear infinite;
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
