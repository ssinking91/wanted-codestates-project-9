<template>
  <section class="search-container">
    <div class="top">
      <div class="input-header">
        <span>검색 결과</span>
        <svg
          width="6"
          height="10"
          viewBox="0 0 6 10"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M1 1L5 5L1 9"
            stroke="#727272"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </div>
      <div v-if="selectCompany">
        <button class="reset-button" @click="removeSelectedCompany">
          <p>{{ selectCompany }}</p>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            x="0px"
            y="0px"
            viewBox="0 0 330 330"
          >
            <g id="XMLID_28_">
              <path
                fill="#d2d2d2"
                id="XMLID_29_"
                d="M165,0C120.926,0,79.492,17.163,48.328,48.327c-64.334,64.333-64.334,169.011-0.002,233.345
		C79.49,312.837,120.926,330,165,330c44.072,0,85.508-17.163,116.672-48.328c64.334-64.334,64.334-169.012,0-233.345
		C250.508,17.163,209.072,0,165,0z M239.246,239.245c-2.93,2.929-6.768,4.394-10.607,4.394c-3.838,0-7.678-1.465-10.605-4.394
		L165,186.213l-53.033,53.033c-2.93,2.929-6.768,4.394-10.607,4.394c-3.838,0-7.678-1.465-10.605-4.394
		c-5.859-5.857-5.859-15.355,0-21.213L143.787,165l-53.033-53.033c-5.859-5.857-5.859-15.355,0-21.213
		c5.857-5.857,15.355-5.857,21.213,0L165,143.787l53.031-53.033c5.857-5.857,15.355-5.857,21.213,0
		c5.859,5.857,5.859,15.355,0,21.213L186.213,165l53.033,53.032C245.104,223.89,245.104,233.388,239.246,239.245z"
              />
            </g>
          </svg>
        </button>
      </div>
    </div>
    <div class="search-bar">
      <input
        class="company-name"
        type="text"
        placeholder="기업명을 검색하세요"
        :value="inputValue"
        @keyup.enter="onEnterHandler"
        @focus="onFocusHandler"
        @blur="onBlurHandler"
        @keyup="onKeyupHandler"
      />
    </div>
  </section>
</template>

<script>
export default {
  props: [
    'showMessage',
    'inputValue',
    'selectCompany',
    'resetSearch',
    'showDropdown',
    'hideDropdown',
    'setInputValue',
  ],
  methods: {
    onEnterHandler(e) {
      this.$emit('setCompanyName', e.target.value);
      document.querySelector('.company-name').blur();
    },
    removeSelectedCompany() {
      this.resetSearch();
    },
    onFocusHandler() {
      this.$emit('showDropdown');
    },
    onBlurHandler() {
      this.$emit('hideDropdown');
    },
    onKeyupHandler(e) {
      // console.log(e.target.value);
      this.$emit('setInputValue', e.target.value);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  /* global style */
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.search-container {
  width: 328px;
  height: auto;
  margin: 20px 16px;
  font-family: 'Noto Sans';
}
.search-container .top {
  width: 100%;
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}
.input-header {
  font-size: 16px;
  font-weight: 700;
  color: #727272;
  display: flex;
  align-items: center;
}
.input-header > span {
  line-height: 100%;
  margin-right: 8px;
}
.input-header > svg {
}
.reset-button {
  display: inline-flex;
  background: none;
  border: none;
  cursor: pointer;
}
.reset-button > p {
  font-size: 14px;
  color: #727272;
}
.reset-button > svg {
  width: 16px;
  height: 16px;
  margin-left: 12px;
}
.search-bar {
  width: 100%;
  height: 48px;
  padding: 12px 16px;
  background-color: #f8f8f8;
  border: 1px solid #f2f2f2;
  border-radius: 4px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.search-bar > input {
  width: 296px;
  height: 20px;
  line-height: 20px;
  color: #121212;
  font-size: 14px;
  font-weight: 400;
  border: none;
  background-color: inherit;
}
.search-bar > input:focus {
  outline: none;
}
.search-bar > input::placeholder {
  color: #b2b2b2;
}
</style>
