<template>
  <div class="w-full h-full">
    <Searchbox @fetch-data="handleFetchData" />
    <div class="mt-8">
      <div v-if="fetchingData">
        <Loading></Loading>
      </div>
      <div v-else-if="error">
        <Error />
      </div>
      <div v-else class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <div>
          <CurrentWeather :weatherData="weatherData" :location="location" />
        </div>
        <div class="lg:col-span-2">
          <div>
            <HourlyWeather :hourlyWeatherData="weatherData.hourly" />
          </div>
          <div class="mt-6">
            <DailyWeather :dailyWeatherData="weatherData.daily" />
          </div>
        </div>
      </div>
    </div>
    <!-- <div v-if="weatherData" class="w-full h-full mt-8 flex justify-center sm:justify-end">
      <img class="w-48 h-24" src="../assets/icons/weather.svg" alt="Weather" />
    </div> -->
  </div>
</template>

<script>
import axios from 'axios';

import Searchbox from '../components/Searchbox';
import CurrentWeather from '../components/CurrentWeather';
import HourlyWeather from '../components/HourlyWeather';
import DailyWeather from '../components/DailyWeather';
import Loading from '../components/Loading';
import Error from '../components/Error';

export default {
  name: 'HomePage',
  components: {
    Searchbox,
    CurrentWeather,
    HourlyWeather,
    DailyWeather,
    Loading,
    Error
  },
  data() {
    return {
      fetchingData: false,
      weatherData: null,
      location: null,
      error: false
    };
  },
  async mounted() {
    this.fetchWeatherdata();
  },
  methods: {
    fetchWeatherdata: async function(query = '') {
      this.fetchingData = true;
      const params = {
        url: process.env.VUE_APP_API_BASE_URL,
        methos: 'get',
        params: {
          query,
          unit: 'metric'
        }
      };
      try {
        const res = await axios(params);

        this.weatherData = res.data.data.weatherData;
        this.location = res.data.data.location;
        this.fetchingData = false;
      } catch (err) {
        console.log('Get current weather failed: ', err);
        this.fetchingData = false;
        this.error = true;
      }
    },
    handleFetchData: function(query) {
      this.fetchWeatherdata(query);
    }
  }
};
</script>
