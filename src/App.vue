<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import cdplayer from "./components/cdplayer.vue";
</script>

<template>
  <div>
    <cdplayer />
  </div>
</template>

<style>
.nes-container.with-title > .title {
  display: table;
  padding: 0 0.5rem;
  margin: -1.8rem 0 1rem;
  font-size: 1rem;
  background-color: rgb(234 179 8 / var(--tw-bg-opacity));
}
</style>
