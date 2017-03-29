<template>
  <div>
    <h4>View Data for Specific Date</h4>
    <input v-on:input="selected()" type="date" ref="dayPicked"/><br/>
    <button v-on:click="viewAll()">View All Data</button>
    <canvas ref="chart" :width="1000" :height="10000"></canvas>
  </div>
</template>

<script>
import Chart from 'chart.js'
import numClicks from '../../fe-demo.json'

export default {
  name: 'chart',
  data: () => ({
    chart: '',
    gradient: null
  }),
  methods: {
    sorter: function () {
      numClicks.sort(function (a, b) {
        return (new Date(a[0]).getTime() - new Date(b[0]).getTime())
      })
      var dayTime = numClicks.map((daytime) => daytime[0])
      this.dataPoints = dayTime
      var click = numClicks.map((numClick) => numClick[1])
      this.numOfClicks = click
    },
    selected: function () {
        this.chart.destroy()
        this.$refs.chart.height = "500"
        console.log(this.$refs.dayPicked.value)
        var datePart = this.$refs.dayPicked.value.match(/\d+/g),
        year = datePart[0].substring(0,4),
        month = datePart[1], day = datePart[2];
        var day = month+'-'+day+'-'+year
        var allDays = numClicks.filter((dayPicked) => dayPicked[0].match(day))
        var dayTime = allDays.map((daytime) => daytime[0])
        this.dataPoints = dayTime
        var click = allDays.map((numClick) => numClick[1])
        this.numOfClicks = click
        this.createChart()
      },
      viewAll: function () {
        this.chart.destroy()
        this.$refs.chart.height = "10000"
        numClicks.sort(function (a, b) {
          return (new Date(a[0]).getTime() - new Date(b[0]).getTime())
        })
        var dayTime = numClicks.map((daytime) => daytime[0])
        this.dataPoints = dayTime
        var click = numClicks.map((numClick) => numClick[1])
        this.numOfClicks = click
        this.createChart()
      },
    createChart () {
      this.gradient = this.$refs.chart.getContext('2d').createLinearGradient(0, 0, 1264, 0)
      this.gradient.addColorStop(0, '#2196f3')
      this.gradient.addColorStop(0.5, '#80719e');
      this.gradient.addColorStop(1, '#f44336');

      this.chart = new Chart(this.$refs.chart, {
        type: 'horizontalBar',
        data: {
          labels: this.dataPoints,
          datasets: [{
            label: '# of Clicks',
            backgroundColor: this.gradient,
            hoverBackgroundColor: "#524972",
            data: this.numOfClicks
          }]
        },
        option: {
          legend: {labels:{fontColor:"white"}}
        }
      }, {responsive: true, maintainAspectRatio: false})
    }
  },
  mounted () {
    this.sorter()
    this.createChart()
  },
  beforeDestroy () {
    this.chart.destroy()
  }
}
</script>
