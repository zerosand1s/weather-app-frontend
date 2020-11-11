<template>
  <div id="app" class="w-full h-screen py-12 bg-blue-100">
    <div class="w-auto h-full mx-4 sm:mx-10 md:mx-16 lg:mx-24">
      <HomePage />
    </div>
    <Footer />
  </div>
</template>

<script>
import HomePage from './pages/Home';
import Footer from './components/Footer';

export default {
  name: 'App',
  components: {
    HomePage,
    Footer
  }
};
</script>

<style>
#app {
  font-family: 'Lato', sans-serif;
}
</style>
