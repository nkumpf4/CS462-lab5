<template>
  <div class="flex flex-row justify-center">
    <div class="p-8 mx-4 flex flex-col justify-center bg-white rounded shadow">
      <h1 class="text-7xl">{{ currentTemp }}°F</h1>
    </div>
    <div class="mx-4 flex flex-col space-between">
      <div class="p-4 mb-4 text-center bg-white rounded shadow">
        <h1 class="text-xl font-semibold">Temperature Log</h1>
        <div>{{ log }}</div>
      </div>
      <div class="p-8 mt-4 text-center bg-white rounded shadow">
        <h1 class="text-xl font-semibold">Threshold Violations</h1>
        <div>{{ violations }}</div>
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
    }, 3000);
  },
  methods: {
    getTemps() {
      fetch("https://random-data-api.com/api/number/random_number")
        .then(response => response.json())
        .then(
          json => (this.currentTemp = json.number.toString().substring(0, 2))
        );
    },
    getViolations() {
      fetch("https://random-data-api.com/api/number/random_number?size=10")
        .then(response => response.json())
        .then(
          json =>
            (this.violations = json.map(el =>
              el.number.toString().substring(0, 2)
            ))
        );
    }
  }
};
</script>
