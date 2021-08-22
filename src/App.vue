<template>
  <main>
    <sound-player />

    <p>
      by: Nurul Huda
    </p>
  </main>
</template>

<script setup>
import SoundPlayer from './components/SoundPlayer.vue'

// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/master/active-rfcs/0040-script-setup.md
</script>

<style>
  body, html {
    font-family: 'Roboto', sans-serif;
    font-weight: 500;
  }
</style>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}
</style>