<template>
  <div
    id="current-weather"
    class="w-auto h-auto px-4 py-2 grid grid-rows-5 rounded-lg text-gray-900 border border-gray-400 shadow-xl bg-white"
  >
    <div class="flex justify-left items-start text-3xl tracking-wider">
      <div>{{ location && location.city && location.city.length ? location.city : '' }}</div>
    </div>
    <div class="row-span-2 flex justify-left items-start">
      <!-- <img class="w-20 h-20 sm:w-24 sm:h-24 object-cover" :src="iconURL" alt="x" /> -->
      <div class="">
        <div class="text-6xl tracking-wide">
          <div>{{ weatherData.current.temp }}°C</div>
        </div>
        <div class="flex justify-left text-sm leading-8">
          <div>{{ weatherData.current.weather[0].main }}</div>
        </div>
        <div class="flex justify-left text-sm">
          <div class="tracking-wider">Feels like:</div>
          <div class="ml-2">{{ weatherData.current.feels_like }}°C</div>
        </div>
      </div>
    </div>
    <div class="row-span-2 grid grid-cols-2 gap-2">
      <div class="flex flex-col justify-center items-start">
        <div class="flex items-center text-xs sm:text-sm leading-10">
          <div class="flex items-center">
            <img class="w-4 h-4" src="../assets/icons/high.svg" alt="High" />
            <div class="ml-2 tracking-wider">High:</div>
          </div>
          <div class="ml-2">{{ weatherData.daily[0].temp.max.toFixed(0) }}°C</div>
        </div>
        <div class="flex items-center text-xs sm:text-sm leading-10">
          <div class="flex items-center">
            <img class="w-4 h-4" src="../assets/icons/humidity.svg" alt="Humidity" />
            <div class="ml-2 tracking-wider">Humidity:&nbsp;</div>
          </div>
          <div class="ml-2">{{ weatherData.current.humidity }}</div>
        </div>
        <div class="flex items-center text-xs sm:text-sm leading-10">
          <div class="flex items-center">
            <div class="text-xs font-bold cursor-default">UV</div>
            <div class="ml-2 tracking-wider">UV Index:&nbsp;</div>
          </div>
          <div class="ml-2">{{ weatherData.current.uvi }}</div>
        </div>
        <div class="flex items-center text-xs sm:text-sm leading-10">
          <div class="flex items-center">
            <img class="w-4 h-4" src="../assets/icons/sunrise.svg" alt="Sunrise" />
            <div class="ml-2 tracking-wider">Sunrise:&nbsp;</div>
          </div>
          <div class="ml-2">{{ sunrise }}</div>
        </div>
      </div>
      <div class="flex flex-col justify-center items-start">
        <div class="flex items-center text-xs sm:text-sm leading-10">
          <div class="flex items-center">
            <img class="w-4 h-4" src="../assets/icons/low.svg" alt="Low" />
            <div class="ml-2 tracking-wider">Low:&nbsp;</div>
          </div>
          <div class="ml-2">{{ weatherData.daily[0].temp.min.toFixed(0) }}°C</div>
        </div>
        <div class="flex items-center text-xs sm:text-sm leading-10">
          <div class="flex items-center">
            <img class="w-4 h-4" src="../assets/icons/visibility.svg" alt="Visibility" />
            <div class="ml-2 tracking-wider">Visibility:&nbsp;</div>
          </div>
          <div class="ml-2">{{ weatherData.current.visibility / 1000 }} km</div>
        </div>
        <div class="flex items-center text-xs sm:text-sm leading-10">
          <div class="flex items-center">
            <img class="w-4 h-4" src="../assets/icons/wind.svg" alt="Wind" />
            <div class="ml-2 tracking-wider">Wind:&nbsp;</div>
          </div>
          <div class="ml-2 flex items-center">
            <span>{{ weatherData.current.wind_speed }} m/s</span>
            <!-- <span class="ml-2 text-xs"><img class="w-4 h-4" :src="windDirectionIcon" alt="W"/></span> -->
          </div>
        </div>
        <div class="flex items-center text-xs sm:text-sm leading-10">
          <div class="flex items-center">
            <img class="w-4 h-4" src="../assets/icons/sunset.svg" alt="Sunset" />
            <div class="ml-2 tracking-wider">Sunset:&nbsp;</div>
          </div>
          <div class="ml-2">{{ sunset }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const dayjs = require('dayjs');

export default {
  name: 'CurrentWeather',
  props: ['weatherData', 'location'],
  computed: {
    sunrise: function() {
      return dayjs(this.weatherData.current.sunrise * 1000).format('HH:mm A');
    },
    sunset: function() {
      return dayjs(this.weatherData.current.sunset * 1000).format('HH:mm A');
    },
    iconURL: function() {
      return `http://openweathermap.org/img/wn/${this.weatherData.current.weather[0].icon}@2x.png`;
    },
    windDirectionIcon: function() {
      let icon = '';
      const windDeg = this.weatherData.current.wind_deg;

      if (windDeg === 0 || windDeg === 360) {
        icon = '../assets/icons/northerly.svg';
      } else if (windDeg > 0 && windDeg < 90) {
        icon = '../assets/icons/north-easterly.svg';
      } else if (windDeg === 90) {
        icon = '../assets/icons/easterly.svg';
      } else if (windDeg > 90 && windDeg < 180) {
        icon = '../assets/icons/south-easterly.svg';
      } else if (windDeg === 180) {
        icon = '../assets/icons/southerly.svg';
      } else if (windDeg > 180 && windDeg < 270) {
        icon = '../assets/icons/south-westerly.svg';
      } else if (windDeg === 270) {
        icon = '../assets/icons/westerly.svg';
      } else if (windDeg > 270 && windDeg < 360) {
        icon = '../assets/static/north-westerly.svg';
      } else {
        icon = '';
      }

      console.log('I: ', icon);

      return icon;
    }
  }
};
</script>

<style scoped>
#current-weather {
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
