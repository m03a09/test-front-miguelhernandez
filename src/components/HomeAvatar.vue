<template>
    <div>
        <h1 class="text-amber-300 pb-10">Search Avatar</h1>
        <div class="grid grid-cols-2 gap-4 pb-5">
            <div>
                <input class="text-center bg-blue-400 h-full rounded placeholder:text-white placeholder:text-center"
                    placeholder="Enter text" v-model="searchAvatar">
            </div>
            <div>
                <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded w-full" @click="search">
                    Search
                </button>
            </div>
        </div>
        <ErrorAvatar :errorMessage="errorMessage" :showError="showError" @changeShowError="changeShowError" />
        <AvatarSearch />
        <TableAvatar :avatars="avatars" />
      <div>
        <BarChart v-if="dataLoaded" :avatarsData="chartData"/>
      </div>
    </div>
</template>
<script>
import TableAvatar from './TableAvatar.vue';
import AvatarSearch from './AvatarSearch.vue';
import ErrorAvatar from './ErrorAvatar.vue';
import BarChart from './BarChart.vue';
import axios from 'axios';

export default {
    name: "HomeAvatar",
    data() {
        return {
            avatars: [],
            searchAvatar: '',
            isLooking: false,
            errorMessage: '',
            showError: false,
            chartData: {
                labels: [''],
                datasets: []
            },
          dataLoaded: false
        };
    },
    components: { TableAvatar, AvatarSearch, ErrorAvatar, BarChart },
    mounted() {
      const ctx = document.getElementById('myChart');
        axios.get('https://api.github.com/users')
            .then(async response => {
                this.avatars = response.data.slice(0, 10);
                await this.processAvatars();
            })
            .catch(error => {
                console.error('Error al obtener los datos:', error);
            });
    },
    methods: {
        async search() {
            if (this.searchAvatar.length > 3 && this.searchAvatar.toLowerCase() !== 'doublevpartners') {
                this.validateSearchMinimumFourChar();
                try {
                    const response = await axios.get('https://api.github.com/search/users?q=' + this.searchAvatar);
                    this.avatars = response.data.items.slice(0, 10);

                } catch (error) {
                    console.error('Error al obtener los datos:', error);
                }
            } else {
                this.showError = true
                this.errorMessage = "Minimum 4 characters and you cannot search for “double partners”.";
            }
        },
        validateSearchMinimumFourChar() {
            if (this.searchAvatar.length === 0) {
                this.isLooking = false;
            } else {
                this.isLooking = true;
            }
        },
        changeShowError() {
            this.showError = !this.showError
        },
        async processAvatars() {
            for (const element of this.avatars) {
              axios.get('https://api.github.com/users/' + element.login).then(response => {
                    let newDataset = {
                        label: response.data.login,
                        data: [response.data.followers],
                    };
                    this.chartData.datasets.push(newDataset)
                  if(this.chartData.datasets.length ===10){
                    this.dataLoaded = true
                  }
                })
            }
        }
    }

}
</script>
