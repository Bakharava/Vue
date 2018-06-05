<template>
    <div class="weather">
        <div v-bind:class="[ 'weather__background', color]">
            <div class="weather__settings fa fa-cog"></div>
            <div class="weather__city">{{weatherData.location.city}}</div>
            <div class="weather__country">{{weatherData.location.country}}</div>
            <div class="weather__degree">{{weatherData.ttl}} {{weatherData.units.temperature}}</div>
            <div class="weather__date">{{weatherData.item.condition.date}}</div>
        </div>
        <div class="weather__temperature">
            <div class="weather__today">Today: <span>{{weatherData.item.forecast[0].high}}-{{weatherData.item.forecast[0].low}}</span></div>
            <div class="weather__tomorrow">Tomorrow: <span>{{weatherData.item.forecast[1].high}}-{{weatherData.item.forecast[1].low}}</span></div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        name: "Weather",
        consumerKey: 'dj0yJmk9d0dGaHZlNTM2WUthJmQ9WVdrOVprRndkbFJWTkRnbWNHbzlNQS0tJnM9Y29uc3VtZXJzZWNyZXQmeD1kNw--',
        weatherUrl: 'https://query.yahooapis.com/v1/public/yql?q=select * from weather.forecast where woeid in (select woeid from geo.places(1) where text="London")&format=json',
        data() {
            return {
                weatherData: [],
                date: '',
                color: ''
            }
        },
        mounted() {
            this.getWeather();
            this.getDate();
            this.getClass();
        },
        methods: {
            getWeather() {
                axios.get(`https://query.yahooapis.com/v1/public/yql?q=select * from weather.forecast where woeid in (select woeid from geo.places(1) where text="London")&format=json`)
                    .then(res => {
                    this.weatherData = res.data.query.results.channel;
                    console.log(this.weatherData)
                }).catch((error) => {
                    console.log(error);
                });
            },
            getDate() {
                let date = new Date();
                console.log(date.getHours());
                return this.date = date.getTime();
            },
            getClass() {
                if(this.date > 6 && this.date < 12) {
                    this.class = 'morning'
                } else  if(this.date > 12 && this.date < 19) {
                    this.color = 'afternoon'
                } else {
                    this.color = 'night'
                }
                return this.color;
            }
        }
    }
</script>

<style src="./Weather.less"></style>
