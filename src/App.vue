<template>
  <header>
    <h1>My Photo Gallery</h1>
  </header>
  
  <div class="app">
    <CameraDisplay />
  </div>

</template>

<script>
import CameraDisplay from './components/CameraDisplay.vue';

export default {
  name: 'app',
  components: {
    CameraDisplay
  }
}
</script>

<style>
header h1{
  font-family: Arial, Helvetica, sans-serif;
  font-size: 2.5em;
  text-align: center;
  font-weight: 600;
  color: transparent;
  background-image: linear-gradient(to left, #0051ff, #a3e2ff);
  background-clip: text;
  -webkit-background-clip: text;
}
.app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width: 100%;
}
</style>