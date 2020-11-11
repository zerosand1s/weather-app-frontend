<template>
  <div
    id="daily-weather"
    class="w-auto h-auto px-2 py-2 rounded-lg text-gray-900 border border-gray-400 shadow-xl bg-white"
  >
    <div class="flex overflow-scroll divide-x">
      <div v-for="dw in dailyWeatherData" :key="dw.dt" class="px-2">
        <Weather :data="dw" :hourly="false" :daily="true" />
      </div>
    </div>
  </div>
</template>

<script>
import Weather from './Weather';

export default {
  name: 'DailyWeather',
  props: ['dailyWeatherData'],
  components: {
    Weather
  }
};
</script>

<style scoped>
#daily-weather {
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
