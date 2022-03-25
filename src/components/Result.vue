<template>
  <div id="result-container">
    <div class="result-title">
      <div class="sub-title">M Y&nbsp;&nbsp; R E S U L T</div>
      <div class="main-title">나의 결과는?</div>
    </div>
    <div class="v-bg"></div>
    <div v-for="(score, idx) in user" :key="idx" class="graph-container">
      <div class="ratio">
        <span class="score" :style="selectScoreColor(score)">{{ score }}</span>

        <span class="total" :style="selectTotalColor(score)">/10</span>
      </div>
      <div class="tendency left" :style="selectTendencyColor(score)">
        {{ tendencies[idx][0] }}
      </div>
      <div class="chart-wrapper">
        <div class="chart-bg">
          <div class="h-bg"></div>
        </div>
        <BarChart
          :userScore="user[idx]"
          :companyScore="getCompanyScore(idx)"
          :selectCompany="selectCompany"
          :currentTab="currentTab"
        />
      </div>
      <div class="tendency right" :style="selectTendencyColor(10 - score)">
        {{ tendencies[idx][1] }}
      </div>
      <div class="ratio">
        <span class="score" :style="selectScoreColor(10 - score)">{{
          10 - score
        }}</span>
        <span class="total" :style="selectTotalColor(10 - score)">/10</span>
      </div>
    </div>
  </div>
</template>

<script>
import referenceData from '../ReferenceData';
import BarChart from '../components/BarChart.vue';

const tendencies = [
  ['적극성', '수동성'],
  ['자신감', '신중함'],
  ['책임감', '무심함'],
  ['개인성향', '조직성향'],
  ['수평사고', '위계사고'],
];
export default {
  name: 'App',
  data() {
    return {
      user: referenceData.user,
      companyData: undefined,
      tendencies: tendencies,
    };
  },
  methods: {
    selectTendencyColor(num) {
      let color = 'color:#3bbe70';
      if (num < 5) {
        color = 'color:#000';
      }
      return color;
    },
    selectScoreColor(num) {
      let color = 'color:#538035';
      if (num < 5) {
        color = 'color:#000';
      }
      return color;
    },
    selectTotalColor(num) {
      let color = 'color:#538035';
      if (num < 5) {
        color = 'color:#7f7e7f';
      }
      return color;
    },
    getCompanyScore(idx) {
      if (!this.companyData) return 0;
      return this.companyData[idx];
    },
  },
  components: { BarChart },
  props: {
    selectCompany: String,
    currentTab: Number,
  },

  beforeUpdate() {
    switch (this.selectCompany) {
      case '삼성전자':
        console.log('check', referenceData.삼성전자);
        this.companyData = referenceData.삼성전자;
        break;
      case '카카오':
        this.companyData = referenceData.카카오;

        break;
      case 'LG':
        console.log('check', referenceData.LG);
        this.companyData = referenceData.LG;
        break;
      default:
        this.companyData = [0, 0, 0, 0, 0];
        break;
    }
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
#result-container {
  width: 360px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}
.result-title {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 118px;
  background-color: #fff;
}
/* @font-face {
  font-family: Agenor;
  src: url('../assets/font/Agenor-Regular/Agenor-Regular.ttf');
} */
.sub-title {
  font-family: Agenor;
  font-size: 12px;
  line-height: 16.8px;
  font-weight: 700;
}
.main-title {
  font-family: Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue',
    sans-serif;
  font-size: 36px;
  line-height: 50.4px;
  font-weight: 700;
}
.result-graph {
  width: 339px;
  height: 202px;
  background-color: rgba(0, 0, 0, 0.199);
}
.graph-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 12px;
  width: 310px;
  height: 40px;
}
.ratio {
  text-align: center;
  width: 37px;
  font-weight: 700;
}
.ratio .total {
  font-size: 10px;
}
.tendency {
  width: 55px;
  padding: 0 1px;
}
.tendency.left {
  text-align: right;
}
.tendency.right {
  text-align: left;
}
.chart-wrapper {
  margin-top: 8px;
  overflow: hidden;
  height: 30px;
}
.chart-bg {
  position: absolute;
  width: 110px;
  height: 40px;
}
.h-bg {
  position: absolute;
  width: 110px;
  height: 10px;
  border-bottom: 1px solid #d2d1d2;
}
.v-bg {
  position: absolute;
  top: 140px;
  width: 1px;
  height: 170px;
  border-left: 1px solid #d2d1d2;
}
</style>
