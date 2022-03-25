<template>
  <div id="container">
    <NavBar />
    <Search
      :inputValue="inputValue"
      @setCompanyName="setCompanyName"
      :selectCompany="selectCompany"
      :resetSearch="resetSearch"
      @showMessage="showMessage"
      @showDropdown="showDropdown"
      @hideDropdown="hideDropdown"
      @setInputValue="setInputValue"
    />
    <AutoComplete
      v-if="isDropdownVisible"
      :companies="companies"
      @setCompanyName="setCompanyName"
      :inputValue="inputValue"
      :dropdownItems="dropdownItems"
    />
    <MessageBox v-if="isMessageVisible" />

    <div class="catBox">
      <img src="../assets/catImg.png" class="catImg" />
      <PantagonChart :selectCompany="selectCompany" :currentTab="currentTab" />
    </div>

    <div class="tabContainer">
      <CategoryTab
        :tabs="tabs"
        :currentTab="currentTab"
        @changeCurrentTab="changeCurrentTab"
      />
    </div>
    <Result :selectCompany="selectCompany" :currentTab="currentTab" />
  </div>
</template>
<script>
import referenceData from '../ReferenceData';
import Result from '../components/Result.vue';
import CategoryTab from '../components/CategoryTab.vue';
import PantagonChart from '../components/PantagonChart.vue';
import Search from '../components/Search.vue';
import MessageBox from '../components/MessageBox.vue';
import NavBar from '../components/NavBar.vue';
import AutoComplete from '../components/AutoComplete.vue';

export default {
  name: 'App',

  data() {
    return {
      user: referenceData.user,
      samsung: referenceData.samsungElectronics,
      kakao: referenceData.kakao,
      lg: referenceData.lgCNS,
      selectCompany: '',
      companies: ['삼성전자', '카카오', 'LG'],
      inputValue: '',
      currentTab: 0,
      tabs: [
        {
          name: '모두',
          icon: {
            src: require('../assets/select1.png'),
            alt: 'companyMe',
          },
        },
        {
          name: '본인',
          icon: {
            src: require('../assets/select2.png'),
            alt: 'Me',
          },
        },
        {
          name: '회사',
          icon: {
            src: require('../assets/select3.png'),
            alt: 'company',
          },
        },
      ],
      isMessageVisible: false,
      msgTimeoutID: {},
      isDropdownVisible: false,
      dropdownItems: ['삼성전자', '카카오', 'LG'],
    };
  },

  methods: {
    changeCurrentTab(i) {
      this.currentTab = i;
    },
    showMessage() {
      // 이전 이벤트로 인해 메시지창이 이미 띄워져 있으면 이벤트 실행하지 않고 리턴
      if (this.isMessageVisible) {
        return;
      }
      if (this.msgTimeoutID) {
        clearTimeout(this.msgTimeoutID);
      }
      this.isMessageVisible = true;

      this.msgTimeoutID = setTimeout(() => {
        this.isMessageVisible = !this.isMessageVisible;
      }, 1500);
    },
    setCompanyName(word) {
      // 기업명을 검색하면
      word = word.toUpperCase();
      if (this.companies.indexOf(word) !== -1) {
        this.inputValue = word;
        this.selectCompany = word;
        this.changeCurrentTab(0);
        document.querySelector('.company-name').blur();
      } else {
        // '기업 정보가 없습니다' 메시지 창 띄우기
        this.showMessage();
      }
    },
    setInputValue(val) {
      this.inputValue = val;
      // 입력값에 따라 드롭다운 아이템 리스트 필터링 (입력된 글자 포함하는 단어만 리스트에 담기)
      const newItems = this.companies.filter(
        (name) => name.indexOf(this.inputValue) > -1,
      );
      this.dropdownItems = newItems;
    },
    resetSearch() {
      this.selectCompany = '';
      this.inputValue = '';
    },
    showDropdown() {
      this.isDropdownVisible = true;
    },
    hideDropdown() {
      setTimeout(() => {
        this.isDropdownVisible = false;
      }, 150);
    },
    setDropdownItems() {
      const newItems = this.companies.filter((name) =>
        name.indexOf(this.inputValue),
      );
      console.log(newItems);
      this.dropdownItems = newItems;
    },
  },

  components: {
    Search,
    MessageBox,
    PantagonChart,
    Result,
    CategoryTab,
    NavBar,
    AutoComplete,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
#container {
  width: 360px;
  margin: 0 auto;
  /* background-color: rgba(255, 192, 203, 0.249); */
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-bottom: 50px;
}
.title {
  height: 72px;
}
.flex-space-between {
  width: 100%;
  padding: 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.search-title {
  height: 62px;
  padding: 20px 16px;
}

input {
  width: 328px;
  height: 48px;
  border-radius: 4px;
  border: none;
  background-color: #f8f8f8;
  margin-bottom: 20px;
}
input::placeholder {
  color: #b2b2b2;
}
.graph {
  background-color: rgba(128, 128, 128, 0.256);
  width: 100%;
  height: 381px;
}

.tabContainer {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 360px;
  height: 84px;
  top: 381px;
  padding: 20px, 16px, 20px, 16px;
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
.result-graph {
  width: 339px;
  height: 202px;
  background-color: rgba(0, 0, 0, 0.199);
}

.catBox {
  width: 100%;
  height: auto;
  position: relative;
  padding: 0 20px;
}

.catImg {
  width: 54px;
  height: 54px;
  position: absolute;
  top: 54%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 9;
}
</style>
