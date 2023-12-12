<template>
  <q-page
    class="flex flex-center"
    style="align-items: center; text-align: center"
  >
    <section class="section flex" id="section1" style="justify-content: center">
      <div id="backG">
        <div>
          <div id="starsContainer">
            <div id="stars"></div>
            <div class="container" style="width: 100%">
              <div class="row">
                <q-card class="my-card">
                  <q-card-section>
                    <q-select
                      rounded
                      borderless
                      v-model="city"
                      :options="data.cities"
                      label="Cidades"
                      class="search"
                      placeholde="Escolha a cidade"
                    />
                  </q-card-section>
                  <q-card-section>
                    <div>
                      Tempo:
                      {{ this.cityInfo.tempo }}
                    </div>
                    <div>Temperatura: {{ this.cityInfo.temperatura }}</div>
                    <div>Vento: {{ this.cityInfo.vento }}</div>
                    <div>Humidade: {{ this.cityInfo.humidade }}</div>

                    <q-btn @click="this.a()">Aaaa</q-btn>
                  </q-card-section>
                </q-card>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </q-page>
</template>

<script>
import axios from "axios";
import json from "src/pages/city.json";

export default {
  data() {
    return {
      api_key: "56c9fef1a5ee34473015f53ff30f06fb",
      url_base: "https://api.openweathermap.org/data/2.5/",
      weather_icon: "http://openweathermap.org/img/wn/",
      city: "Curitiba",
      data: json,
      weather: {},
      cityInfo: [],
    };
  },
  async mounted() {
    const stars = document.getElementById("stars");
    const backG = document.getElementById("backG");
    function generateStar(randomAngle = Math.floor(Math.random(100) * 360)) {
      const star = document.createElement("div");
      star.classList.add("singleStar");
      const left = Math.floor(Math.random() * 100);
      const top = Math.floor(Math.random() * 100);
      const size = Math.floor(Math.random() * 4);
      star.style.width = size + "px";
      star.style.height = size + "px";
      star.style.left = (left / 100) * 100 + "%";
      star.style.top = (top / 100) * 100 + "%";
      stars.appendChild(star);
      star.addEventListener("mouseover", () => {
        star.style.opacity = "0.3";
        setTimeout(() => {
          star.style.display = "none";
        }, 1000);
      });
    }
    for (let i = 0; i <= 300; i++) {
      generateStar();
    }
    setTimeout(() => {
      const h1 = document.getElementById("twoSec");
      stars.removeChild(h1);
    }, 2000);
  },
  created() {
    this.fetchWeather();
  },
  methods: {
    async fetchWeather() {
      let response = await axios.get(
        `${this.url_base}weather?q=${this.city}&units=metric&APPID=${this.api_key}`
      );
      this.setResults(response.data);
    },
    setResults(returnedResponse) {
      this.weather = returnedResponse;
      this.cityInfo = {
        tempo: this.weather.weather[0].description,
        temperatura: this.weather.main.temp,
        vento: this.weather.wind.speed,
        humidade: this.weather.main.humidity,
      };
    },
    a() {
      console.log(process.env.VUE_APP_APIKEY);
    },
  },
};
</script>

<style lang="scss">
.container {
  width: 100%;
  align-items: center;
  text-align: center;
  margin-top: 9.375rem;
}

.section {
  max-height: 4500px !important;
  min-height: 2450px !important;
  height: 100% !important;
}

.my-card {
  width: 600px;
  height: 600px;
}

.search {
  width: 200px;
}
</style>
