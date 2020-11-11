<template>
  <div class="w-auto h-12 flex flex-col justify-between items-center">
    <div class="text-lg tracking-wider font-light">Loading</div>
    <div class="w-48 h-2 mt-8 flex items-center rounded-full bg-gray-400 border border-gray-500">
      <div id="loading" class="w-4 h-full rounded bg-indigo-800"></div>
    </div>
    <div class="w-full h-full mt-8 flex justify-center">
      <img class="w-96 h-96" src="../assets/icons/weather.svg" alt="Weather" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Loading'
};
</script>

<style scoped>
#loading {
  animation: loading-animation 2s linear infinite alternate;
}

@keyframes loading-animation {
  0% {
    transform: translatex(0px);
  }
  25% {
    transform: translatex(44px);
  }
  50% {
    transform: translatex(88px);
  }
  75% {
    transform: translatex(132px);
  }
  100% {
    transform: translatex(176px);
  }
}
</style>
