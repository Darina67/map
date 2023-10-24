<template>
  <div id="app">
    <yandex-map/>
  </div>
</template>

<script>
import YandexMap from "./components/YandexMap";

export default {
  name: "App",
  components: {
    YandexMap
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
