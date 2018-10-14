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

              <div class="prayerTimes__info--date">
                <span v-if="!hijri">{{formattedDate}}</span>
                <span v-else >19th Muharram 1440</span>

                <!-- <Date /> -->

                <button class="btn--arrow btn--sync">
                  <i class="material-icons" @click="toggleHijri">sync</i>
                </button>

              </div>

          </div>
          <div class="prayerTimes__table">
            <div class="prayerTimes__table__row">
              <div class="">Fajr</div>
              <div class="">{{data.times[date].fajr}}</div>
            </div>
            <div class="prayerTimes__table__row">
              <div class="">Sunrise</div>
              <div class="">{{data.times[date].sunrise}}</div>
            </div>
            <div class="prayerTimes__table__row">
              <div class="">Dhur</div>
              <div class="">{{data.times[date].dhuhr}}</div>
            </div>
            <div class="prayerTimes__table__row">
              <div class="">Asr</div>
              <div class="">{{data.times[date].asr}}</div>
            </div>
            <div class="prayerTimes__table__row">
              <div class="">Maghrib</div>
              <div class="">{{data.times[date].magrib}}</div>
            </div>
            <div class="prayerTimes__table__row">
              <div class="">Isha</div>
              <div class="">{{data.times[date].isha}}</div>
            </div>
          </div>
          <div class="btn-group prayerTimes__btns">
            <button class="btn--arrow btn--left" @click="changeDate('left')" v-if="date !== startOfMonth">
              <i class="material-icons">keyboard_arrow_left</i>
            </button>
            <button class="btn--arrow btn--right" @click="changeDate('right')" v-if="date !==  endOfMonth">
              <i class="material-icons">keyboard_arrow_right</i>
            </button>
          </div>
      </section>
      <span style="justify-self: center; background: #fff; border-radius: 2px; color: #333;
      padding: 2rem;" v-if="msg">{{msg}}</span>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
import animate from "animate.css";

export default {
  data() {
    return {
      loading: true,
      data: null,
      date: "",
      msg: null,
      startOfMonth: null,
      endOfMonth: null,
      hijri: false
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
    },
    formattedDate() {
      const formattedDate = moment(this.date).format("dddd, DD MMM");
      return formattedDate;
    }
  },
  methods: {
    toggleHijri() {
      this.hijri = !this.hijri;
    },
    getDate() {
      return moment().format("YYYY-MM-DD");
    },
    changeDate(direction) {
      if (direction === "right") {
        this.date = moment(this.date)
          .add(1, "day")
          .format("YYYY-MM-DD");
        this.alert(this.date);
      }

      if (direction === "left") {
        this.date = moment(this.date)
          .subtract(1, "day")
          .format("YYYY-MM-DD");
        this.alert(this.date);
      }
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
    },
    setupMonthRange() {
      // this.day = moment(this.date).format("DD");
      this.startOfMonth = moment()
        .startOf("month")
        .format("YYYY-MM-DD");

      this.endOfMonth = moment()
        .endOf("month")
        .format("YYYY-MM-DD");
    }
  },
  mounted() {
    this.date = this.getDate();
    this.getCalendar();
    this.setupMonthRange();
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
  font-weight: 100;
  /* padding: 2rem 0; */
}

.prayerTimes__countdown * {
  margin: 0.7rem;
}

.prayerTimes__countdown h1 {
  width: max-content;
  font-weight: 400 !important;
  font-size: 2rem;
}

.prayerTimes__wrapper {
  border: 1px solid #eeeeee;
  margin: 0 1.5rem 0 1.5rem;
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

.prayerTimes__info--date {
  display: grid;
  grid-template-columns: repeat(2, max-content);
}

.prayerTimes__info--date span {
  font-size: 1rem;
}

.btn--sync {
  padding: 0 1rem;
}
.btn--sync i {
  font-size: 1.3rem;
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

@media only screen and (min-width: 768px) {
  .prayerTimes__wrapper {
    min-width: 600px;
    max-width: 800px;
    justify-self: center;
  }

  .prayerTimes__container {
    margin: 2rem 0;
    grid-gap: 60px;
  }
}

@media only screen and (min-width: 1200px) {
  .prayerTimes__wrapper {
    min-width: 800px;
  }
}
</style>
