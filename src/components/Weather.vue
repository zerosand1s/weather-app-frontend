<template>
  <div
    class="w-32 h-auto p-2 flex flex-col items-center border-t-4 border-blue-700 border-opacity-0 hover:border-opacity-100 hover:shadow-md"
  >
    <div class="text-sm tracking-wide leading-10">{{ hourly ? getHour(data.dt) : getDay(data.dt) }}</div>
    <div class="text-xl tracking-wide leading-10">{{ hourly ? data.temp : data.temp.day }}°C</div>
    <div class="text-sm tracking-wide leading-10">{{ data.weather[0].main }}</div>
    <div v-if="daily">
      <div class="flex mt-2 text-xs">
        <span>H: {{ data.temp.max.toFixed(0) }}°C</span>
        <span class="ml-2">L: {{ data.temp.min.toFixed(0) }}°C</span>
      </div>
      <div class="mt-4 text-xs">
        <div class="flex justify-center">
          <img class="w-4 h-4" src="../assets/icons/sunrise.svg" alt="Sunrise" />
          <div class="ml-2">{{ getSunrise(data.sunrise) }}</div>
        </div>
        <div class="mt-2 flex justify-center">
          <img class="w-4 h-4" src="../assets/icons/sunset.svg" alt="Sunset" />
          <div class="ml-2">{{ getSunset(data.sunset) }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const dayjs = require('dayjs');
const weekday = require('dayjs/plugin/weekday');
dayjs.extend(weekday);

export default {
  name: 'Weather',
  props: ['data', 'hourly', 'daily'],
  data() {
    return {
      days: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']
    };
  },
  methods: {
    getHour: function(timestamp) {
      return dayjs.unix(timestamp).format('HH:mm');
    },
    getDay: function(timestamp) {
      const day = dayjs(timestamp * 1000).weekday();
      return this.days[day] + ', ' + dayjs(timestamp * 1000).format('DD/MM');
    },
    getSunrise: function(timestamp) {
      return dayjs(timestamp * 1000).format('HH:mm');
    },
    getSunset: function(timestamp) {
      return dayjs(timestamp * 1000).format('HH:mm');
    }
  }
};
</script>

<style></style>
