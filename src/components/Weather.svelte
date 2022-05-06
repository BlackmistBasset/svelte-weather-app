<script lang="ts">
import type { WeatherInfoInterface } from "../interfaces/Weather";

import Alert from "./Alert.svelte"
import Loading from "./Loading.svelte"
import WeatherInfo from "./WeatherInfo.svelte"

    const key = '477df6a8e5d0ed44d223ebaa63c3b2c6'

    let city = ''

    const getWeatherData = async (city:string = "Buenos Aires") => {
        const baseUrl = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&lang=es&appid=${key}`

        if(city.trim() === "") {
            throw new Error("Por favor ingresá el nombre de una ciudad.")
        }

        const res: Response = await fetch(baseUrl)
        
        const data: WeatherInfoInterface = await res.json()

        if(data.cod !== 200) {
            throw new Error("La ciudad no fue encontrada")
        }
            return data
    }
 
    let promise = getWeatherData()   

    const handleSubmit = () => {
        promise = getWeatherData(city)
        city = ''
    }
</script>

<div class="container weather-app">
    <div class="row">
        <div class="col-12 mb-3">
            <form on:submit|preventDefault="{handleSubmit}">
                <p class="label-buscador">Ingresar ciudad: </p>
                <div class="container contenedor-inputs">
                    <input bind:value="{city}" type="text" class="form-control me-2" />
                    <input type="submit" value="Buscar" class="btn btn-primary "/>
                </div>
            </form>
        </div> 

        {#await promise}
            <Loading />
        {:then data} 
            <WeatherInfo {data} />       

        {:catch err}
            <Alert {err} />

        {/await}
    </div>
</div>

<style>
    .label-buscador {
        font-weight: bold;
        margin: 15px;
    }

    .contenedor-inputs {
        display: flex;
        width: 70%;
    }

    .weather-app {
        max-width: 900px;
        height: 400px;
        border: 4px solid #0d6efd;
        border-radius: 25px;
        padding: 30px 20px;
        margin-top: 20px;
    }
</style>