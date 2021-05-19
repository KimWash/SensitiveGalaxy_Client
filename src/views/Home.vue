<template>
  <div class="home">
    <h1 class="title" style="padding-top: 24px; text-align: center">
      SensitiveGalaxy
    </h1>
    <div class="tile is-ancestor" style="margin-bottom: 0px">
      <div class="tile is-vertical">
        <div class="tile">
          <div class="tile is-parent is-vertical">
            <article class="tile is-child notification is-primary">
              <p class="title is-size-4-mobile">실내 온도</p>
              <p class="subtitle">{{ temperature }} ºC</p>
            </article>
            <article class="tile is-child notification is-warning">
              <p class="title is-size-4-mobile">실내 습도</p>
              <p class="subtitle">{{ humidity }} %</p>
            </article>
            <article class="tile is-child notification is-warning">
              <p class="title is-size-4-mobile">실내 조도</p>
              <p class="subtitle">{{ light }} %</p>
            </article>
          </div>
        </div>
      </div>
    </div>
    <p style="text-align: right">최근 업데이트: {{ lastUpdate }}</p>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      temperature: 0,
      humidity: 0,
      light:0,
      lastUpdate: "",
    };
  },
  created() {
    axios.get("http://localhost:8000/api/data").then((res) => {
      const data = res.data;
      if (data.success) {
        this.temperature = data.data.temperature;
        this.humidity = data.data.humidity;
        this.light = data.data.light;
        this.lastUpdate = new Date(Date.parse(data.data.lastUpdated));
      }
    });
  },
};
</script>
