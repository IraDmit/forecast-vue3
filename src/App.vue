<script setup>
import appMainInfo from './components/app-mainInfo.vue'
import appCoords from './components/app-coords.vue'
import appForecast from './components/app-forecast.vue'
import appRain from './components/app-rain.vue'
import { ref, onMounted } from 'vue'
import { API_KEY, API_URL } from './constants'

const city = ref('Tolyatti')
let weatherInfo = ref({})

const fetchData = () => {
  fetch(`${API_URL}/weather?q=${city.value}&appid=${API_KEY}&units=metric`)
    .then((res) => res.json())

    .then((responce) => {
      weatherInfo.value = responce
    })
}

onMounted(() => {
  fetchData()
})
const changeCity = (name) => {
  city.value = name
  fetchData()
}
</script>

<template>
  <div class="page">
    <main class="main">
      <div class="container">
        <div class="laptop">
          <div class="sections">
            <app-main-info @changeCity="changeCity" :weather="weatherInfo" />

            <app-forecast :highlights="weatherInfo" />
          </div>
          <div class="sections">
            <app-coords :coords="weatherInfo.coord" />

            <app-rain :humidity="weatherInfo.main" />
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<style lang="scss"></style>
