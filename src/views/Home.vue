<template>
  <div class="flex flex-col items-center justify-center">
    <div
      class="flex flex-col justify-center p-8 mx-4 mb-4 bg-white rounded shadow"
    >
      <h1 class="text-7xl">{{ currentTemp }}°F</h1>
    </div>
    <div class="flex flex-row mx-4 space-between">
      <div
        class="p-8 mx-2 overflow-auto text-center bg-white rounded shadow h-96"
      >
        <h1 class="mb-2 text-xl font-semibold">Temperature Log</h1>
        <div>
          <div v-for="(entry, index) in log" :key="index">
            {{ entry.timestamp }} : {{ entry.temperature }}
          </div>
        </div>
      </div>
      <div
        class="p-8 mx-2 overflow-auto text-center bg-white rounded shadow h-96"
      >
        <h1 class="mb-2 text-xl font-semibold">Threshold Violations</h1>
        <div>
          <div v-for="(entry, index) in violations" :key="index">
            {{ entry.timestamp }} : {{ entry.temperature }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentTemp: 75,
      log: [],
      violations: []
    };
  },
  mounted() {
    this.getTemps();
    this.getViolations();

    setInterval(() => {
      this.getTemps();
      this.getViolations();
    }, 7500);
  },
  methods: {
    getTemps() {
      fetch(
        "http://192.168.11.11:3000/sky/cloud/ckkuoyesy00fawbu804nkd1eo/temperature_store/temperatures"
      )
        .then(response => (this.log = response.json()))
        .then(json => {
          this.log = json.reverse();
          this.currentTemp = this.log[0].temperature;
        });
    },
    getViolations() {
      fetch(
        "http://192.168.11.11:3000/sky/cloud/ckkuoyesy00fawbu804nkd1eo/temperature_store/threshold_violations"
      )
        .then(response => response.json())
        .then(json => (this.violations = json.reverse()));
    }
  }
};
</script>
