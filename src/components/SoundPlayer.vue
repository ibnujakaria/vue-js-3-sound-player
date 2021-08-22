<template>
  <div>
    <section
      class="audio-player"
    >
      <button
        v-if="!isPlaying"
        @click="play()"
      >
        <i class="ri-play-fill"></i>
      </button>
      <button
        v-else
        @click="pause()"
      >
        <i class="ri-pause-fill"></i>
      </button>

      <div class="duration">
        0:{{ currentTimeHuman }} / 0:{{ duration }}
      </div>

      <div class="progress">
        <div
          class="value"
          :style="{
            width: `${currentTime / duration * 100}%`
          }"
        />
      </div>
    </section>
  </div>
</template>

<script>
import { computed, ref } from '@vue/runtime-core'

export default {
  setup() {
    const audio = new Audio('/natural.wav')
    const duration = ref(0)
    const currentTime = ref(0)
    const isPlaying = ref(false)

    const play = () => audio.play()
    const pause = () => audio.pause()

    audio.addEventListener('playing', () => {
      isPlaying.value = true
    })

    audio.addEventListener('pause', () => {
      isPlaying.value = false
    })

    audio.addEventListener('timeupdate', e => {
      currentTime.value = audio.currentTime
    })

    audio.addEventListener('durationchange', e => {
      duration.value = audio.duration
    })

    const currentTimeHuman = computed(() => {
      const time = Math.floor(currentTime.value)

      return time < 10 ? `0${time}` : time
    })

    return {
      audio,
      play,
      pause,
      duration,
      currentTime,
      isPlaying,
      currentTimeHuman,
    }
  },
}
</script>

<style scoped>
@import 'remixicon/fonts/remixicon.css';

.audio-player {
  background: #14a800;
  width: 20rem;
  color: white;
  padding: .75rem 1.25rem;
  border-radius: 5rem;
  font-weight: 600;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  box-shadow: 0 .25rem .5rem rgba(0, 0, 0, 0.1);
}

.audio-player button {
  border: none;
  transition: all .3s ease-in-out;
  background: transparent;
  color: white;
  width: 1.75rem;
  aspect-ratio: 1 / 1;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  font-size: 1.15rem;
}

.audio-player button:hover {
  background: rgba(0, 0, 0, 0.1);
}

.audio-player .progress {
  flex-grow: 1;
  height: 3px;
  border-radius: 2px;
  background-color: white;
  position: relative;
}

.audio-player .duration {
  font-size: .9rem;
}

.audio-player .progress .value {
  height: 3px;
  left: 0;
  top: 0;
  border-radius: 2px;
  background-color: rgb(255, 190, 93);
}
</style>
