<template>
  <div class="row">
    <div class="col-12" id="weather">
      <h1 class="text-center font-weight-bolder text-primary">My Weather App</h1>
    </div>
    <br /><br /><br />
    <div class="col-12">
      <form action="#" @click.prevent="">
        <div class="form-inline justify-content-center">
          <input
            type="text"
            placeholder="city name + Enter"
            class="form-control"
            v-model="city"
          />
          <div class="input-group-append">
            <button
              class="mx-3 btn btn-outline-info"
              type="submit"
              @click="getWeaderData"
            >
              get weather
            </button>
          </div>
        </div>
      </form>
    </div>
    <div class="col-12">
      <transition-group
        enter-active-class="animate__animated animate__fadeInUp"
      >
        <div
          id="item"
          class="col-12 bg-info my-2"
          v-for="i in info"
          :key="i.name"
        >
          <div class="weather-data">
            <div class="weather-stats">
              <div>
                <span class="location"
                  ><h2 class="font-weight-bold text-light">
                    {{ i.name }}
                  </h2></span
                >
              </div>
            </div>
            <div class="weather-temp">
              <h4 class="text-warning">{{ i.temp }}K = {{ i.c }} C</h4>
            </div>
            <img
              class="weather-icon"
              :src="`http://openweathermap.org/img/wn/${i.icon}@2x.png`"
            />
            <div class="weather-stats">
              <h4 class="text-dark">
                {{ i.description }}
              </h4>
            </div>
          </div>
        </div>
      </transition-group>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "weather",
      city: "",
      info: []
    };
  },
  methods: {
    getWeaderData() {
      this.$http
        .get(
          `http://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=7f4baa8cd7eee1b75bf7f8345d38a6f4`
        )
        .then(Response => {
          return Response.json();
        })
        .then(data => {
          const obj = {
            temp: data.main.temp,
            c: Math.ceil(parseInt(data.main.temp) - 273.15),
            name: data.name,
            icon: data.weather[0].icon,
            description: data.weather[0].description
          };
          // console.log(data);
          this.info.push(obj);
          this.city = "";
        });
    }
  }
};
</script>

<style scoped>
#item {
  border-radius: 1em;
}
.weather-data {
  display: flex;
  align-items: center;
  margin-top: 20px;
  margin-left: 20px;
  padding: 20px;
}

.weather-icon {
  flex-grow: 1;
}

.weather-stats {
  flex-grow: 8;
  text-align: left;
  padding-left: 20px;
}

.weather-stats .location {
  font-size: 30px;
}

.weather-temp {
  flex-grow: 1;
  font-size: 35px;
}

img {
  width: 70px;
}
</style>
