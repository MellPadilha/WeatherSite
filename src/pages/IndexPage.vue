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
                      v-model="model"
                      :options="data.cities"
                      label="Cidades"
                      class="search"
                      placeholde="Escolha a cidade"
                    />
                  </q-card-section>
                  <q-card-section></q-card-section>
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
import json from "src/pages/city.json";

export default {
  name: "IndexPage",
  data() {
    return {
      apiUrl: `https://api.openweathermap.org/data/2.5/weather?&appid=${process.env.API_KEY}&units=metric`,
      response: "",
      data: json,
      model: "Curitiba",
    };
  },
  mounted() {
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
  methods: {
    async getTemperature(city) {
      this.response = await fetch(this.apiUrl + `&q=${city}`);
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
