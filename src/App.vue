<template>
  <div id="app">
    <header class="header">
      <h3 class="header__brand">Salah Times</h3>
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
  /* font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif; */
  /* font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif; */
  font-family: "Roboto";
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
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
  padding: 1.35rem 1rem;
}

.header__brand {
  margin: 0;
  color: #fff;
  font-weight: 400;
  font-size: 1.25rem;
}

.footer {
  display: grid;
  grid-template-columns: 1fr 1fr;
  padding: 1.5rem 2rem;
}

.footer__poweredBy {
  justify-self: end;
}

.btn-group {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  padding: 0 0 1rem 0;
  justify-self: center;
  /* background: #f7f7f7ee; */
}

.btn--arrow {
  border: 0;
  background: none;
  color: #000000;
  padding: 0.3rem 1rem;
  border-radius: 2px;
  cursor: pointer;
  text-transform: uppercase;
  font-weight: 600;
  letter-spacing: 3px;
  outline: 0;
}

.btn--arrow i {
  font-size: 2rem;
  color: #478dfc;
}

.btn:hover {
  background: #fff;
  color: #333;
  transition: 0.3s;
}

.btn--right {
  grid-column: 2;
}

.btn--left {
  grid-column: 1;
}
</style>
