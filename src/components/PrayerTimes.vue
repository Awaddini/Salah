<template>
  <div class="prayer-times">
    <div v-if="loading" class="loading">
        Loading...
    </div>
    <div v-else>
        <!-- Loop through each date object containing the times for that day -->
        <div v-for="(prayerTime, property, i) in data.times" :key="i">
            <!-- Get todays prayer times -->
            <div v-if="getTimesByDate(property)">
                <!-- loop through the object containing todays prayer times -->
                <div v-for="(value, propertyName, index) in prayerTime" :key="index" >
                    <!-- Remove unwanted properties like jamat -->
                    <div v-if="filterdata(propertyName)" class="row">
                            <div class="title">{{propertyName}}</div>
                            <span class="test">{{value}}</span>
                            <hr>
                    </div>
                </div>
            </div>
        </div>
        <div>

        </div>
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
        }
    },
    methods: {
        filterdata (propertyName) {
            if (propertyName !== 'date' && propertyName !== 'fajr_jamat' 
                && propertyName !== 'dhuhr_jamat' 
                && propertyName !== 'asr_jamat'
                && propertyName !== 'magrib_jamat' 
                && propertyName !== 'isha_jamat'
                && propertyName !== 'asr_2'
                && propertyName !== 'sunrise'){
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
                return true;
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

    /* .uppercase {
        text-transform: capitalize;
        margin: 0.5rem 0;
    } */

    .title {
        font-size: 1.5rem;
        font-weight: 300;
        margin: 0.6rem 0;
        text-transform: capitalize;
        color: rgb(36, 36, 36);
    }

    .fab {
        width: 56px;
        height: 56px;
        border-radius: 30%;
    }

    .fab-icon {
        color: #fff;
    }
</style>
