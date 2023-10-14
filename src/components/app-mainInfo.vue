<template>
  <section class="section section-left">
    <div class="info">
      <div class="city-inner">
        <input
          type="text"
          class="search"
          v-model="city"
          @keypress.enter="emit('changeCity', city)"
          :placeholder="weather?.name"
        />
      </div>

      <div class="summary" v-if="weather?.weather">
        <div
          :style="`background-image: url('./src/assets/img/weather-main/${weather?.weather[0].description}.png')`"
          class="pic-main"
        ></div>
        <div class="weather">
          <div class="temp">{{ Math.round(weather?.main?.temp) }} °C</div>
          <div class="weather-desc text-block">
            {{ bigLetter(weather?.weather[0].description) }}
          </div>
        </div>
        <div class="city text-block">
          {{ weather?.name || 'Paris' }}, {{ weather?.sys?.country || 'FR' }}
        </div>
        <div class="date text-block">{{ formatDate }}</div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import { bigLetter } from '../utils'
const { modelValue } = defineProps({ modelValue: String, weather: Object })
const emit = defineEmits('changeCity')

const city = ref(modelValue)
const date = new Date()
const formatDate = date.toLocaleString('en-US', {
  year: 'numeric',
  month: 'long',
  day: 'numeric',
  weekday: 'short'
})
</script>

<style lang="scss" scoped></style>
