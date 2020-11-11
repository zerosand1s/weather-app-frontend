<template>
  <div class="w-full h-full flex flex-col justify-between items-center">
    <h1 class="text-3xl text-gray-900 font-bold tracking-wider">Oops, Something went wrong</h1>
    <img class="w-96 h-96" src="../assets/icons/error.svg" alt="Error" />
    <h4 class="text-base text-gray-900 tracking-wide">
      Looks like there was an error while fetching weather data. Please try again later.
    </h4>
  </div>
</template>

<script>
export default {
  name: 'Error'
};
</script>
