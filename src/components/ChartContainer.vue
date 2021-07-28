<template>
  <div class="container">
    <div  class="chart-container">
      <h1 class="title">Продажи</h1>
      <Chart
          class="chart"
          v-if="loaded"
          :chartData="chartData"
          :options="options"
      />
    </div>
    <div class="legend-container">
      <div class="legend">
        <LegendItem
            v-for="(dataset, idx) of chartData.datasets"
            :key="idx"
            @hide-chart="hideChart"
            v-bind:idx="idx"
            v-bind:dataset="dataset"
            v-bind:color="dataset.backgroundColor !== 'transparent'
                  ? dataset.backgroundColor
                  : dataset.borderColor"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Chart from './Chart.vue'
import LegendItem from './LegendItem'

export default {
  name: 'ChartContainer',
  components: { Chart, LegendItem },
  data: () => ({
    loaded: true,
  }),
  computed: {
    chartData() {
      return {
        labels: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20],
        datasets: [
          {
            type: 'line',
            label: 'Средний чек',
            backgroundColor: 'transparent',
            borderColor: '#A18CD1',
            borderWidth: 1.4,
            hidden: false,
            tension: 0,
            radius: 0,
            categoryPercentage: 0.99,
            barPercentage: 0.99,
            yAxisID: 'line-y-axis',
            data: [50, 70, 30, 76, 139, 140, 222, 249, 180, 1800, 215, 127, 47, 50, 70, 30, 76, 39, 40, 22],
            // data: [0],
          },
          {
            type: 'line',
            label: 'Что-то там',
            backgroundColor: 'transparent',
            borderColor: '#448dc4',
            borderWidth: 1.4,
            hidden: false,
            tension: 0,
            radius: 0,
            categoryPercentage: 0.99,
            barPercentage: 0.99,
            yAxisID: 'line-y-axis',
            data: [222, 249, 180, 800, 215, 127, 50, 70, 30, 76, 139, 140, 47, 50, 70, 30, 76, 39, 40, 22],
            // data: [0],
          },
          {
            label: 'Возвраты',
            backgroundColor: '#FF7576',
            categoryPercentage: 0.99,
            hidden: false,
            barPercentage: 0.99,
            yAxisID: 'bar-y-axis',
            data: [0, 0, 0, 20, 10, 12, 33, 22, 4, 0]
          },
          {
            label: 'Заказы в приложении',
            backgroundColor: '#80E0E5',
            categoryPercentage: 0.99,
            barPercentage: 0.99,
            hidden: false,
            yAxisID: 'bar-y-axis',
            data: [0, 0, 0, 40, 39, 10, 40, 39, 80, 40]
          },
          {
            label: 'Покупки в магазине',
            backgroundColor: '#FFDA93',
            categoryPercentage: 0.99,
            barPercentage: 0.99,
            hidden: false,
            yAxisID: 'bar-y-axis',
            data: [0, 0, 0, 26, 39, 10, 52, 39, 80, 40]
          },
        ]
      }
    },
    options() {
      return {
        responsive: true,
        maintainAspectRatio: false,
        legend: {
          display: false,
        },
        tooltips: {
          mode: 'index',
          position: 'average',
        },
        scales: {
          xAxes: [{
            stacked: true,
            gridLines: {
              drawTicks: false,
              zeroLineWidth: 2,
              zeroLineColor: 'black',
              z: 1,
            },
            ticks: {
              fontColor: 'black',
              fontFamily: 'Rubik, sans-serif',
              fontStyle : 300,
              fontSize: 12,
              padding: 8,
            }
          }],
          yAxes: [{
            id: 'bar-y-axis',
            stacked: true,
            gridLines: {
              drawTicks: false,
              zeroLineWidth: 2,
              zeroLineColor: 'black',
              z: 1,
            },
            ticks: {
              suggestedMin: 10,
              suggestedMax: 200,
              fontColor: 'black',
              fontFamily: 'Rubik, sans-serif',
              fontStyle : 300,
              fontSize: 12,
              padding: 8,
            }
          }, {
            id: 'line-y-axis',
            position: 'right',
            gridLines: {
              drawTicks: false,
              zeroLineWidth: 2,
              zeroLineColor: 'black',
              z: 1,
            },
            ticks: {
              suggestedMin: 100,
              suggestedMax: 2000,
              fontColor: 'black',
              fontFamily: 'Rubik, sans-serif',
              fontStyle : 300,
              fontSize: 12,
              padding: 8,
            }
          }]
        }
      }
    }
  },
  mounted () {
    // this.loaded = false
    // try {
    //   const { userlist } = await fetch('/api/userlist')
    //   this.chartData = userlist
    //   this.loaded = true
    // } catch (e) {
    //   console.error(e)
    // }

  },
  methods: {
    hideChart(idx, checked) {
      this.chartData.datasets[idx].hidden = !checked
      this.$children[0].rerender() //called because of non-reactivity
    },
  },
}
</script>
<style>

.container {
  display: flex;
  width: 90vw;
  background-color: aliceblue;
  margin: auto;
  color: #B2B2B2;
  font-family: Rubik, sans-serif;
  border-radius: 20px;
  padding: 20px;
  box-sizing: border-box;
}
.chart-container {
  flex:2 0 400px;
  /*width: 70%;*/
}
.title {
  font-size: 1.5rem;
  text-align: start;
  padding-left: 7%;
}
.chart {
  /*height: 70vh;*/
}
.legend-container {
  flex:1 0 200px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-width: 200px;
}
.legend {
  margin: 40px;
  color: black;
  font-family: Rubik, sans-serif;
  font-style: normal;
  font-weight: 300;
  font-size: 0.8rem;
  display: flex;
  flex-direction: column;
  flex:1 0 200px;
  justify-content: center;
  align-items: start;
}
</style>
