<template>
  <div class="dropdown-container">
    <ul>
      <li
        v-for="(item, i) of dropdownItems"
        v-bind:key="i"
        class="dropdown-item"
        @click="onClickHandler"
      >
        {{ item }}
      </li>
      <li class="no-match" v-if="dropdownItems.length === 0">
        일치하는 기업명이 없습니다
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // dropdownItems: this.companies,
    };
  },
  props: ['companies', 'setCompanyName', 'inputValue', 'dropdownItems'],
  methods: {
    onClickHandler(e) {
      this.$emit('setCompanyName', e.target.textContent);
    },
  },
};
</script>

<style>
.dropdown-container {
  position: absolute;
  top: 176px;
  z-index: 9;
  width: 328px;
  height: auto;
  padding: 10px;
  border: 1px solid #f2f2f2;
  border-radius: 8px;
  background: #fff;
}
.dropdown-item {
  padding: 10px;
  font-size: 14px;
  cursor: pointer;
}
.dropdown-item:hover {
  background: #f8f8f8;
}
.no-match {
  padding: 6px;
  font-size: 12px;
}
</style>
