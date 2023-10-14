<template>
  <v-container>
    <div>{{ $route.query }}</div>

    <tr>
      <td class="pa-5">
        <v-card class="elevation-6">
          <div class="ma-3">
            <p class="font-weight-black">홈런순위</p>
          </div>
          <div class="ma-3"><canvas id="homerun"></canvas></div>
        </v-card>
      </td>
      <td class="pa-6">
        <v-card class="elevation-6">
          <div class="ma-3">
            <p class="font-weight-black">안타순위</p>
          </div>
          <div class="ma-5"><canvas id="hit"></canvas></div>
        </v-card>
      </td>
      <td class="pa-6">
        <v-card class="elevation-6">
          <div class="ma-3">
            <p class="font-weight-black">득점순위</p>
          </div>
          <div class="ma-5"><canvas id="score"></canvas></div>
        </v-card>
      </td>
    </tr>
    <tr>
      <td>
        <v-card class="elevation-6">
          <div class="ma-3">
            <p class="font-weight-black">안타비율</p>
          </div>
          <div style="white-space: nowrap">{{ this.$route.query.teams }}</div>
          <div style="white-space: nowrap">
            {{ this.$route.query.team_hits }}
          </div>
          <div class="ma-4"><canvas id="hit_rate"></canvas></div>
        </v-card>
      </td>
    </tr>
  </v-container>
</template>
<script>
import {
  Chart,
  BarElement,
  BarController,
  LinearScale,
  CategoryScale,
  DoughnutController,
  ArcElement,
} from "chart.js";

Chart.register(
  BarElement,
  BarController,
  LinearScale,
  CategoryScale,
  DoughnutController,
  ArcElement
);

export default {
  methods: {
    updateChart() {
      let homeStatus = Chart.getChart(this.homeChart);
      homeStatus.destroy(); // key change

      let hitStatus = Chart.getChart(this.hitChart);
      hitStatus.destroy();

      let scoreStatus = Chart.getChart(this.scoreChart);
      scoreStatus.destroy();

      let circleStatus = Chart.getChart(this.circleChart);
      circleStatus.destroy();

      this.renderChart();
    },

    renderChart() {
      const config = {
        type: "bar",
        data,
        options: {
          indexAxis: "y",
        },
      };

      const home_ctx = document.getElementById("homerun").getContext("2d");
      var labels = [];
      var data = [];
      var temp = this.$route.query.homerun;
      temp.forEach((e) => {
        let line = e.split(",");
        labels.push(line[1]);
        data.push(line[2]);
      });

      this.homeChart = new Chart(home_ctx, {
        type: "bar",
        data: {
          labels: labels,
          datasets: [
            {
              data: data,
              backgroundColor: [
                "rgba(255, 218, 97, 0.5)",
                "rgba(207, 207, 207, 0.5)",
                "rgba(235, 125, 0, 0.5)",
              ],
            },
          ],
        },
        options: this.opt,
      });

      const hit_ctx = document.getElementById("hit").getContext("2d");
      var labels = [];
      var data = [];
      var temp = this.$route.query.Hit;
      temp.forEach((e) => {
        let line = e.split(",");
        labels.push(line[1]);
        data.push(line[2]);
      });

      this.hitChart = new Chart(hit_ctx, {
        type: "bar",
        data: {
          labels: labels,
          datasets: [
            {
              data: data,
              backgroundColor: [
                "rgba(255, 218, 97, 0.5)",
                "rgba(207, 207, 207, 0.5)",
                "rgba(235, 125, 0, 0.5)",
              ],
            },
          ],
        },
        options: this.opt,
      });
      const score_ctx = document.getElementById("score").getContext("2d");
      var labels = [];
      var data = [];
      var temp = this.$route.query.scorer;
      temp.forEach((e) => {
        let line = e.split(",");
        labels.push(line[1]);
        data.push(line[2]);
      });
      this.scoreChart = new Chart(score_ctx, {
        type: "bar",
        data: {
          labels: labels,
          datasets: [
            {
              data: data,
              backgroundColor: [
                "rgba(255, 218, 97, 0.5)",
                "rgba(207, 207, 207, 0.5)",
                "rgba(235, 125, 0, 0.5)",
              ],
            },
          ],
        },
        options: this.opt,
      });
      let hits = this.$route.query.team_hits;
      hits = hits.map(Number);
      let team = this.$route.query.teams;
      const hits_ctx = document.getElementById("hit_rate").getContext("2d");
      this.circleChart = new Chart(hits_ctx, {
        type: "doughnut",
        data: {
          labels: team,
          datasets: [
            {
              data: hits,
              backgroundColor: [
                "rgba(54, 162, 235, 0.2)",
                "rgba(153, 102, 255, 0.2)",
                "rgba(131, 236, 189, 0.51)",
                "rgba(131, 0, 189, 0.51)",
                "rgba(131, 219, 236, 0.51)",
                "rgba(128, 0, 255, 0.5)",
                "rgba(255, 99, 132, 0.2)",
                "rgba(255, 159, 64, 0.2)",
                "rgba(255, 205, 86, 0.2)",
                "rgba(75, 192, 192, 0.2)",
              ],
              // hoverOffset: 11,
            },
          ],
        },
        options: {
          plugins: {
            datalabels: {
              formatter: (value) => {
                return value + "%";
              },
            },
          },
        },
      });
    },
  },
  watch: {
    $route: function (to, from) {
      this.updateChart();
      deep: true;
    },
  },
  data() {
    return {
      homeChart: null,
      hitChart: null,
      scoreChart: null,
      circleChart: null,
      opt: {
        indexAxis: "y",

        barThickness: 15,
        borderWidth: 0,
      },
    };
  },
  mounted() {
    this.renderChart();
  },
};
</script>
