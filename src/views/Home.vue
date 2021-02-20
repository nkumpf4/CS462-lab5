<template>
  <div class="flex flex-row justify-center">
    <div class="p-4 mx-4 text-center bg-white rounded shadow">
      <h1 class="text-xl font-semibold">Temperature Log</h1>
    </div>
    <div class="p-8 mx-4 text-center bg-white rounded shadow">
      <h1 class="text-5xl">{{ currentTemp }}°F</h1>
    </div>
    <div class="p-4 mx-4 text-center bg-white rounded shadow">
      <h1 class="text-xl font-semibold">Threshold Violations</h1>
    </div>
  </div>
</template>

<script>
import { Chart } from "chart.js";

export default {
  data() {
    return {
      currentTemp: 75,
    };
  },
  methods: {
    drawChart() {
      /* eslint-disable no-unused-vars */
      var ctx = document.getElementById("myChart");
      var myChart = new Chart(ctx, {
        type: "line",
        data: {
          labels: [
            new Date(-2),
            new Date(-1),
            new Date(0),
            new Date(1),
            new Date(2),
          ],

          datasets: [
            {
              label: "Temperature",
              data: [76, 75, 77, 78, 79],
              borderWidth: 1,
              backgroundColor: "rgba(135, 206, 235, .5)",
            },
            {
              label: "Threshold",
              data: [70, 70, 70, 70, 70],
              borderWidth: 1,
              pointRadius: 0,
              borderColor: "rgba(200, 0, 0, 1)",
              fill: false,
            },
          ],
        },
        options: {
          color: ["red", "blue"],
          scales: {
            yAxes: [
              {
                ticks: {
                  beginAtZero: true,
                },
              },
            ],
            xAxes: [
              {
                type: "time",
              },
            ],
          },
        },
      });
      /* eslint-enable no-unused-vars */
    },
  },
};
</script>

<style scoped>
.tes {
  color: rgb(135, 206, 235);
}
</style>
