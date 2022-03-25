<template>
  <BarChart
    @click="test"
    id="bar-chart"
    ref="doughnutRef"
    :chartData="testData"
    :options="options"
    :style="{
      width: '110px',
      height: '50px',
      alignItems: 'center',
      top: '5px',
    }"
  />
</template>

<script>
import { Chart, registerables } from 'chart.js';
import { computed, defineComponent, ref } from 'vue';
import { BarChart } from 'vue-chart-3';
Chart.register(...registerables);

export default defineComponent({
  name: 'Home',

  components: { BarChart },

  props: {
    userScore: Number,
    companyScore: Number,
    selectCompany: String,
    currentTab: Number,
  },
  data() {
    return {
      currentUserScore: this.userScore,
      currentCompanyScore: this.companyScore,
      matchData: 6,
    };
  },
  methods: {
    test() {
      console.log(this.userScore, this.companyScore, this.currentData);
    },
  },

  setup() {
    const data = ref([0, 0]);
    const doughnutRef = ref();
    const options = ref({
      responsive: true,
      plugins: {
        legend: {
          position: 'top',
        },
      },
      indexAxis: 'y',
      scales: {
        y: {
          display: false,
          grid: {
            display: false,
          },
        },
        x: {
          display: false,
          grid: {
            display: false,
          },
          ticks: {
            display: true,
            stepSize: 2,
          },
          min: -10,
          max: 10,
        },
      },
    });

    const testData = computed(() => ({
      labels: ['적극적인', '자신있는', '책임있는', '개인주의', '수평적인'],
      datasets: [
        {
          data: data.value,
          backgroundColor: ['#6e3cf9', '#ffd966'],
          barThickness: 5,
          bar: { backgroundColor: 'red' },
        },
      ],
    }));

    return { testData, doughnutRef, options };
  },
  // beforeCreate() {
  //   console.log('비포크리에이트', this.companyScore, this.data);
  // },
  // created() {
  //   this.testData.datasets[0].data[1] =
  //     this.companyScore > 5 ? this.companyScore * -1 : this.companyScore;
  //   console.log('크리에이트', this.companyScore, this.data);
  // },
  beforeUpdate() {
    if (this.currentTab === 2) {
      this.testData.datasets[0].data[0] = 0;
    } else {
      this.testData.datasets[0].data[0] =
        this.userScore > 5 ? this.userScore * -1 : this.userScore;
    }

    if (!this.selectCompany || this.currentTab === 1) {
      this.testData.datasets[0].data[1] = 0;
    } else {
      this.testData.datasets[0].data[1] =
        this.companyScore > 5 ? this.companyScore * -1 : this.companyScore;
    }
  },
  beforeMount() {
    // this.testData.datasets.data

    this.testData.datasets[0].data[0] =
      this.userScore > 5 ? this.userScore * -1 : this.userScore;
  },
});
</script>

<style>
#bar-chart {
  display: block;
  width: 100px;
}
.check {
  position: fixed;
  width: 200px;
  z-index: 9;
}
</style>
