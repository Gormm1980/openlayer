<template>
  <div id="app">
    
    <MapLayer/>
  </div>
</template>

<script>
import 'ol/ol.css';
import MapLayer from './components/MapLayer.vue';
export default {
  name: 'App',
  components: {
    MapLayer,
  }
  }

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
