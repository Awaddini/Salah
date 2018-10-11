<template>
  <div id="app">
    <header class="header">
      <h3 class="header__brand">Prayer</h3>
    </header>
    <prayer-times></prayer-times>
    <footer class="footer">
      <span></span>
      <span class="footer__poweredBy">Powered by Allah</span>
    </footer>
  </div>
</template>

<script>
import PrayerTimes from "./components/PrayerTimes.vue";

export default {
  name: "app",
  components: {
    PrayerTimes
  }
};
</script>

<style>
html,
body {
  height: 100%;
  margin: 0;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  /* font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif; */
}

#app {
  min-height: 100%;
  display: grid;
  grid-template-rows: max-content 1fr;
  background: #7c4dff;
  background-image: linear-gradient(#7c4dff, #a537fd);
  color: #fff;
}

.header {
  padding: 1.5rem 2rem;
}

.header__brand {
  margin: 0;
  color: #fff;
  font-weight: 300;
  font-size: 1.3rem;
}

.footer {
  display: grid;
  grid-template-columns: 1fr 1fr;
  padding: 1.5rem 2rem;
}

.footer__poweredBy {
  justify-self: end;
}
</style>
