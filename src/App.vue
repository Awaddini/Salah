<template>
  <div id="app">
    <h1 class="hero-text">Prayer Times</h1>
    <prayer-times></prayer-times>
  </div>
</template>

<script>
import PrayerTimes from './components/PrayerTimes.vue'

export default {
  name: 'app',
  components: {
    PrayerTimes
  }
}
</script>

<style>

html, body{
  height: 100%;
  margin: 0;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
  /* font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif; */
}

.hero-text {
  /* color: #fff; */
}

#app {
  /* background-image: linear-gradient(
  124.5deg,
  rgba(68,125,239,1) 16.5%, rgba(40,108,246,1) 100%
); */

  /* background: red; */
  /* padding: 1rem; */
  min-height: 100%;
  padding: 1rem;

}
</style>
