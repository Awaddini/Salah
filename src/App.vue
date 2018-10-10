<template>
  <div id="app">
    <header class="header-wrapper">
      <h3 class="header-brand">Prayer</h3>
    </header>
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

* {
}

html, body{
  height: 100%;
  margin: 0;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
  /* font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif; */
}

#app {
  /* background-image: linear-gradient(
  124.5deg,
  rgba(68,125,239,1) 16.5%, rgba(40,108,246,1) 100%
); */

  /* background: red; */
  /* padding: 1rem; */
  min-height: 100%;
  display: grid;
  grid-template-rows: max-content 1fr;
  background: #7C4DFF;
  background-image: linear-gradient(#7C4DFF, #A537FD);
  color: #fff;
}

.header-wrapper {
  /* color: #fff; */
  /* background: #612EF0; */
  padding: 1.5rem 2rem;
}

.header-brand {
  margin: 0;
  color: #fff;
  font-weight: 300;
  font-size: 1.3rem;
}
</style>
