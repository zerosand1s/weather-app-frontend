<template>
  <div
    id="hourly-weather"
    class="w-auto h-auto px-2 py-2 rounded-lg text-gray-900 border border-gray-400 shadow-xl bg-white"
  >
    <div class="flex overflow-scroll divide-x">
      <div v-for="hw in hourlyWeatherData" :key="hw.dt" class="px-2">
        <Weather :data="hw" :hourly="true" :daily="false" />
      </div>
    </div>
  </div>
</template>

<script>
import Weather from './Weather';

export default {
  name: 'HourlyWeather',
  props: ['hourlyWeatherData'],
  components: {
    Weather
  }
};
</script>

<style scoped>
#hourly-weather {
  -webkit-animation-name: slideInUp;
  animation-name: slideInUp;
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}
@-webkit-keyframes slideInUp {
  0% {
    -webkit-transform: translateY(70%);
    transform: translateY(70%);
    visibility: visible;
  }
  100% {
    -webkit-transform: translateY(0);
    transform: translateY(0);
  }
}
@keyframes slideInUp {
  0% {
    -webkit-transform: translateY(70%);
    transform: translateY(70%);
    visibility: visible;
  }
  100% {
    -webkit-transform: translateY(0);
    transform: translateY(0);
  }
}
</style>
