<template>
  <Bar id="my-chart-id" :options="chartOptions" :data="avatarsData" />
</template>

<script>
import { Bar } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  name: 'BarChart',
  components: { Bar },
  data() {
    return {
      chartOptions: {
        responsive: true,
        plugins: {
          title: {
            display: true,
            text: 'Followers'
          }
        }
      }
    }
  },
  props: {
    avatarsData: {
      required: true
    }
  }

}
</script>
