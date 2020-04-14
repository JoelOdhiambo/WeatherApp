<template>
  <div class="text-white mb-8">
    <div class="places-input text-gray-800">
      <input type="text" class="w-full" />
    </div>

    <div
      class="weather-container font-sans w-128 max-w-lg rounded-lg overflow-hidden bg-gray-900 shadow-lg mt-4"
    >
      <div class="current-weather flex items-center justify-between px-6 py-8">
        <div class="flex items-center">
          <div>
            <div class="text-6xl" font-semibold>{{currentTemperature.actual}}°C</div>
            <div>{{currentTemperature.feels}}°C</div>
          </div>
          <div class="mx-5">
            <div class="font-semibold">{{currentTemperature.summary}}</div>
            <div>{{location.name}}</div>
          </div>
        </div>
        <div>{{currentTemperature.icon}}</div>
      </div>
      <!-- end current-weather -->

      <div class="future-weather text-sm bg-gray-800 px-6 py-8 overflow-hidden">
        <div class="flex items-center">
          <div class="w-1/6 text-lg text-gray-200">MON</div>
          <div class="w-2/3 px-4 flex items-center">
            <div>icon</div>
            <div class="ml-3">Cloudy with a chance of showers</div>
          </div>
          <div class="w-1/6" text-right>
            <div>5°C</div>
            <div>-2°C</div>
          </div>
        </div>

        <div class="flex items-center mt-8">
          <div class="w-1/6 text-lg text-gray-200">MON</div>
          <div class="w-2/3 px-4 flex items-center">
            <div>icon</div>
            <div class="ml-3">Cloudy with a chance of showers</div>
          </div>
          <div class="w-1/6" text-right>
            <div>5°C</div>
            <div>-2°C</div>
          </div>
        </div>

        <div class="flex items-center mt-8">
          <div class="w-1/6 text-lg text-gray-200">MON</div>
          <div class="w-2/3 px-4 flex items-center">
            <div>icon</div>
            <div class="ml-3">Cloudy with a chance of showers</div>
          </div>
          <div class="w-1/6" text-right>
            <div>5°C</div>
            <div>-2°C</div>
          </div>
        </div>
      </div>
      <!-- end future-weather -->
    </div>
    <!-- end weather-container -->
  </div>
</template>

<script>
export default {
  mounted() {
    this.fetchData();
  },
  data() {
    return {
      currentTemperature: {
        actual: '',
        feels: '',
        summary: '',
        icon: '',
      },
      daily: [],
      location: {
        name: 'Kisumu',
        lat: -0.10221,
        lon: 34.761711,
      }
    }
  },
  methods: {
    fetchData() {
      fetch(`/api/weather?lat=${this.location.lat}&lon=${this.location.lon}`)
        .then(response => response.json())
        .then(data => {
          console.log(data);
          this.currentTemperature.actual = Math.round(data.main.temp)
          this.currentTemperature.feels = Math.round(data.main.feels_like)
          this.currentTemperature.summary = data.weather[0].main
          this.currentTemperature.icon = data.weather[0].icon
        
        
        });
    }
  }
};
</script>
