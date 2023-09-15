<template>
    <div class="flex flex-col flex-1 items-center">
        <!-- Banner -->
        <div v-if="route.query.preview"
        class="text-white p-4 bg-weather-secondary w-full text-center"
        >
            <p>
                You are currentl previewing this city, click the "+" icon to start traking this city.
            </p>
        </div>
        
        <!-- Weather -->
        <div class="flex flex-col items-center text-white py-12">
            <h1 class="text-4xl mb-2"> {{ route.params.city }} </h1>
                <p class="text-sm mb-12">
                    {{ 
                        new Date(weatherData.currentTime).toLocaleDateString(
                            "es-mx",
                            {
                                weekday: "short",
                                day: "2-digit",
                                month: "long"
                            })
                     }}
                     {{ 
                        new Date(weatherData.currentTime).toLocaleTimeString(
                            "es-mx",
                            {
                                timeStyle:"short"
                            }
                        )
                      }}
                </p>
                <p class="text-8xl mb-8">
                    {{ Math.round(weatherData.current.temp) }}&deg;
                </p>
                <p>
                    Feel like 
                    {{ Math.round(weatherData.current.feels_like) }}&deg;
                </p>
                <p class="capitalize"> 
                    {{ weatherData.current.weather[0].description }} 
                </p>
                <img class="w-[150px] h-auto" 
                :src="`https://openweathermap.org/img/wn/${weatherData.current.weather[0].icon}@2x.png`" 
                alt=""
                />
        </div>
    </div>
</template>

<script setup>
import axios from 'axios';
import { useRoute } from 'vue-router';

const key = "4ebb4fe1c25ae1433820a605dd9cee2c";
const route = useRoute();
const getWeatherData = async () => {
    try {
        const weatherData = await axios.get(`https://api.openweathermap.org/data/2.5/onecall?lat=${route.query.lat}&lon=${route.query.lon}&exclude={part}&appid=${key}&units=imperial`);

        // cal current date & time
        const localOffset = new Date().getTimezoneOffset() * 60000;
        const utc = weatherData.data.current.dt * 1000 + localOffset;
        weatherData.data.currentTime =
            utc + 1000 * weatherData.data.timezone_offset;

        // cal hourly weather offset
        weatherData.data.hourly.forEach((hour) => {
            const utc = hour.dt * 1000 + localOffset;
            hour.currentTime = utc + 1000 * weatherData.data.timezone_offset;
        });

        return weatherData.data;
    } catch (err) {
        console.log(err);
    }
}
const weatherData = await getWeatherData();
</script>

<style></style>