<template>
  <div class="prayer-times">
    <div v-if="loading" class="loading">
        Loading...
    </div>
    <div v-else class="prayer-times__container">
        <!-- Loop through each date object containing the times for that day -->

        <section class="prayer-countdown__wrapper">
            <h1>03:55:53</h1>
            <p>Time until next prayer</p>
        </section>
        <section class="prayer-times__wrapper">
            <div class="prayer-info__wrapper">
                <h3>London</h3>
                <span class="prayer-info__date">29 Muharram 1440</span>
            </div>

            <div v-for="(prayerTime, i) in filteredPrayerTimes" :key="i">
                <!-- Get todays prayer times --> 
                <div v-for="(value, propertyName, index) in filteredPrayerTime" :key="index">

                    <div  class="prayer-table__row">
                            <div class="title">{{propertyName}}</div>
                            <span class="test">{{value}}</span>
                    </div>
                </div>
            </div>

        </section>

    </div>
  </div>
</template>

<script>
import axios from 'axios';



export default {
    data () {
        return {
            loading: true,
            data: null
        }
    },
    computed: {
        search () {
            var today = new Date();
            return {
                key: '4f447b24-2597-4a34-a167-0d4013862e61',
                year: '2018',
                month: today.getMonth() + 1
            }
        },
        filteredPrayerTimes () {
            Object.keys(this.data.times).filter(key => !this.getTimesByDate(key))
            .forEach(key => delete this.data.times[key]);
            return this.data.times;
        },
        filteredPrayerTime () {
            const key = Object.keys(this.data.times);
            const filtered = this.data.times[key[0]];
            Object.keys(filtered).filter(propertyName => 
                propertyName == 'date'
                || propertyName == 'fajr_jamat' 
                || propertyName == 'dhuhr_jamat' 
                || propertyName == 'asr_jamat'
                || propertyName == 'magrib_jamat' 
                || propertyName == 'isha_jamat'
                || propertyName == 'asr_2')
            .forEach(key => delete filtered[key])
            return filtered;
        }
    },
    methods: {
        filterdata (propertyName) {
            if (propertyName !== 'date' && propertyName !== 'fajr_jamat' 
                && propertyName !== 'dhuhr_jamat' 
                && propertyName !== 'asr_jamat'
                && propertyName !== 'magrib_jamat' 
                && propertyName !== 'isha_jamat'
                && propertyName !== 'asr_2'){
                return true;
            }
        },
        getTimesByDate (property) {
            var today = new Date();
            var dd = today.getDate();
            var mm = today.getMonth() +1;
            var yyyy =today.getFullYear();

            if (dd < 10) {
                dd = '0' + dd;
            }

            if (mm < 10){
                mm = '0' + mm;
            }

            today = yyyy + '-' + mm + '-' + dd;
            // setting test date below
            // today = '2018' + '-' + '09' + '-' + '30';
            if (today === property){
                return property;
            } else {
                return false;
            }
        }
    },
    mounted () {
        axios
            .get(`https://www.londonprayertimes.com/api/times/?format=json&key=${this.search.key}&year=${this.search.year}&month=${this.search.month}`)
            .then(response => {
                this.data = response.data;
                console.log(this.data)
            })
            .catch(() => console.log(`error: ${this.search}`))
            .finally(() => this.loading = false)
    }

}

</script>

<style scoped>
    .prayer-times {
        display: grid;

    }

    .loading {
        margin-top: 10rem;
        justify-self: center;
    }

    .prayer-times__container{
        display: grid;
        grid-template-rows: max-content max-content;
        margin: 2rem 0;
        grid-gap: 30px;
    }

    .prayer-countdown__wrapper {
        display: grid;
        justify-items: center;
        align-items: center;
        /* padding: 2rem 0; */
    }
    
    .prayer-countdown__wrapper *{
        margin: 0.7rem;
    }

    .prayer-countdown__wrapper h1{
        width: max-content;
        font-weight: 300;
        font-size: 2rem;
    }

    .prayer-times__wrapper{
        border: 1px solid #eeeeee;
        margin: 0 1.5rem 0 1.5rem;
        padding: 1.5rem 1rem;
        display: grid;
        grid-template-rows: max-content 1fr;
        grid-gap: 35px;
        max-height: max-content;
        background: #fff;
        color: #333;
        border-radius: 2px;
    }

    .prayer-info__wrapper {
        display: grid;
        grid-gap: 20px;
        justify-items: center;
    }

    .prayer-info__wrapper * {
        margin: 0;
    }

    .prayer-info__date {
        font-size: 0.75rem;
        font-weight: 600;
    }

    .prayer-table__row {
        display: grid;
        grid-template-columns: 1fr 1fr;
        margin: 1rem 0;
        text-transform: capitalize;
        justify-items: center;
        text-align: start;
    }
</style>
