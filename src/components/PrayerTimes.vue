<template>
  <div class="prayerTimes">
    <!-- Replace loading with spinner or similar -->
    <div v-if="loading" class="loading">
        Loading...
    </div>
    <div v-else class="prayerTimes__container">

      <!-- Static countdown -->
      <section class="prayerTimes__countdown">
          <h1>03:55:53</h1>
          <p>Time until next prayer</p>
      </section>

      <section class="prayerTimes__wrapper">
          <div class="prayerTimes__info">
              <h3>London</h3>
              <!-- Static hijri year below -->
              <span class="prayerTimes__info__date">29 Muharram 1440</span>
          </div>
          <div class="prayerTimes__table">
            <div class="prayerTimes__table__row">
              <div class="">Fajr</div>
              <div class="">{{data.times[currentDate].fajr}}</div>
            </div>
            <div class="prayerTimes__table__row">
              <div class="">Sunrise</div>
              <div class="">{{data.times[currentDate].sunrise}}</div>
            </div>
            <div class="prayerTimes__table__row">
              <div class="">Dhur</div>
              <div class="">{{data.times[currentDate].dhuhr}}</div>
            </div>
            <div class="prayerTimes__table__row">
              <div class="">Asr</div>
              <div class="">{{data.times[currentDate].asr}}</div>
            </div>
            <div class="prayerTimes__table__row">
              <div class="">Maghrib</div>
              <div class="">{{data.times[currentDate].magrib}}</div>
            </div>
            <div class="prayerTimes__table__row">
              <div class="">Isha</div>
              <div class="">{{data.times[currentDate].isha}}</div>
            </div>
          </div>
      </section>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      loading: true,
      data: null,
      currentDate: ""
    };
  },
  computed: {
    search() {
      var today = new Date();
      return {
        key: "4f447b24-2597-4a34-a167-0d4013862e61",
        year: "2018",
        month: today.getMonth() + 1
      };
    }
  },
  methods: {
    getTimesByDate() {
      var today = new Date();
      var dd = today.getDate();
      var mm = today.getMonth() + 1;
      var yyyy = today.getFullYear();

      if (dd < 10) {
        dd = "0" + dd;
      }

      if (mm < 10) {
        mm = "0" + mm;
      }

      return `${yyyy}-${mm}-${dd}`;
    },
    async getCalendar() {
      const { key, year, month } = this.search;
      const response = await axios
        .get(
          `https://www.londonprayertimes.com/api/times/?format=json&key=${key}&year=${year}&month=${month}`
        )
        // Need to catch errors properly
        .catch(() => console.log(`error: ${this.search}`));

      this.data = response.data;
      console.log(this.data);
      this.loading = false;
    }
  },
  mounted() {
    this.currentDate = this.getTimesByDate();
    this.getCalendar();
  }
};
</script>

<style scoped>
.prayerTimes {
  display: grid;
}

.loading {
  margin-top: 10rem;
  justify-self: center;
}

.prayerTimes__container {
  display: grid;
  grid-template-rows: max-content max-content;
  margin: 1rem 0;
  grid-gap: 30px;
}

.prayerTimes__countdown {
  display: grid;
  justify-items: center;
  align-items: center;
  /* padding: 2rem 0; */
}

.prayerTimes__countdown * {
  margin: 0.7rem;
}

.prayer__countdown h1 {
  width: max-content;
  font-weight: 300;
  font-size: 2rem;
}

.prayerTimes__wrapper {
  border: 1px solid #eeeeee;
  margin: 0 1.5rem 0 1.5rem;
  /* padding: 1.5rem 1rem; */
  display: grid;
  grid-template-rows: max-content 1fr;
  /* grid-gap: 10px; */
  max-height: max-content;
  background: #fff;
  color: #333;
  border-radius: 2px;
}

.prayerTimes__info {
  display: grid;
  grid-gap: 15px;
  justify-items: center;
  background: rgba(247, 247, 247, 0.933);
  padding: 1.5rem 1rem;
}

.prayerTimes__info * {
  margin: 0;
}

.prayerTimes__info__date {
  font-size: 0.85rem;
  /* font-weight: 600; */
}

.prayerTimes__table {
  display: grid;
  grid-gap: 30px;
  padding: 2rem 1rem;
}

.prayerTimes__table__row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  text-transform: capitalize;
  text-align: start;
  justify-items: center;
}

.prayerTimes__table__row * {
  /* text-align: center; */
}
</style>
