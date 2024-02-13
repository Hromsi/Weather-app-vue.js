<script>
import axios from 'axios';

export default {
    data() {
        return {
            city: '',
            error: '',
            info: null,
        }
    },
    computed: {
        cityName() {
            return '«' + this.city + '»';
        },
        showTemp() {
            return 'Температура: ' + this.info.main.temp;
        },
        showFeelsLike() {
            return 'Ощущается как: ' + this. info.main.feels_like;
        },
        showMinTemp() {
            return 'Минимальная температура: ' + this.info.main.temp_min;
        },
        showMaxTemp() {
            return 'Маскимальная температура: ' + this.info.main.temp_max;
        },
    },
    methods: {
        getWeather() {
            this.info = null;

            if(this.city.trim().length < 2) {
                this.error = 'Нужно название более одного символа'
                return false
            }

            this.error = '';

            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&lang=ru&appid=1c2701d42e29aeae65336a4e1e19fdec`)
                .then(res => (this.info = res.data))
                .catch(error => (this.error = `Город с названием «${this.city}» не найден!`))
            // this.info = res;
            
            
        }
    }
}
</script>
https://api.openweathermap.org/data/2.5/weather?q=Seattle&appid=1c2701d42e29aeae65336a4e1e19fdec
<template>
    <div class="wrapper">
        <h1>Погодное приложение</h1>
        <p>Узнать погоду в {{ city == '' ? 'вашем городе' : cityName }}</p>
        <input type="text" v-model="city" placeholder="Введите город"/>
        <!-- @input="this.city = $event.target.value" -->
        <button v-if="city != ''" @click="getWeather()">Получить погоду</button>
        <button disabled v-else>Введите название города</button>
        <p class="error">{{ error }}</p>
        <div v-if="info != null">
            <p>{{ showTemp }}</p>
            <p>{{ showFeelsLike }}</p>
            <p>{{ showMinTemp }}</p>
            <p>{{ showMaxTemp }}</p>
        </div>
    </div>
</template>

<style scoped>
.error {
    color: #d03939;
}

.wrapper {
    width: 900px;
    height: 500px;
    border-radius: 50px;
    padding: 20px;
    background: #272727d6;
    box-shadow: 0px 0px 20px #31313194;
    text-align: center;
    color: white;
    font-family: Arial;
}

.wrapper h1 {
    margin-top: 50px;
}

.wrapper p {
    margin-top: 20px;
}

.wrapper input {
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid #110813;
    /* color: #fcfcfc; */
    padding: 5px 8px;
    outline: none;
}

.wrapper input:focus {
    border-bottom: 2px solid #6e2d7d;
    color: white;
}

.wrapper button {
    background: #e3bc4b;
    color: #fff;
    width: 195px;
    border-radius: 10px;
    border: 2px solid #b99935;
    padding: 10px 15px;
    margin-left: 20px;
    cursor: pointer;
    transition: transform 500ms ease;
}

.wrapper button:disabled {
    /* background: #898989; */
    background: #746027;
    color: #fff;
    /* border: 2px solid #272727; */
    cursor: not-allowed;
}

.wrapper button:hover {
    transform: scale(1.05) translateY(-5px);
}
</style>
