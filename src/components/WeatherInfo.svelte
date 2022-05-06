<script lang="ts">
    export let data;
</script>

<div class="animate__animated animate__fadeInUp col-12 col-md-6">
    <h1>
        <img src={`http://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`} alt={`${data.weather[0].main}`}>{data.main.temp} °C
    </h1>
    <h4>Ciudad: <span class="fw-bold">{data.name}, {data.sys.country}</span></h4>
    <h4>Clima: <span class="fw-bold weather-description">{data.weather[0].description}</span></h4>
</div>

<div class="animate__animated animate__fadeInUp col-12 col-md-6 d-flex flex-column justify-content-center">
    <h4 class="mt-3">Mínima: <span class="fw-bold text-primary">{data.main.temp_min} °C</span></h4>
    <h4 class="mt-3">Máxima: <span class="fw-bold text-danger">{data.main.temp_max} °C</span></h4>
</div>  

<style>

    .weather-description {
        text-transform: capitalize;
    }
    
</style>