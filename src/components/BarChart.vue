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
            /*chartData: {
              labels: ['January', 'February', 'March'],
              datasets: [
                {
                  label: 'a',
                  data: [1, 2, 3],
                },
                {
                  label: 'b',
                  data: [4, 5, 6],
                }
              ]
            },*/
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
            required:true
        }
    }

}
</script>
