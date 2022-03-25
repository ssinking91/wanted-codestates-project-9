<template>
  <ul class="tabBox">
    <li
      v-for="(tab, i) in tabs"
      v-bind:key="i"
      @click="changeCurrent(i)"
      :class="{ current: currentTab === i }"
    >
      <img :src="tab.icon.src" :alt="tab.icon.alt" />
      <span>{{ tab.name }}</span>
    </li>
  </ul>
</template>

<script>
export default {
  props: ['tabs', 'currentTab'],
  data() {
    return {};
  },
  methods: {
    changeCurrent(i) {
      this.$emit('changeCurrentTab', i);
    },
  },
};
</script>

<style>
.tabBox {
  width: 325px;
  height: 45px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 4px;
  background-color: #f2f2f2;
}

.tabBox li {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 107.33px;
  height: 43px;
  background-color: #f2f2f2;
  font-size: 12px;
  border: 1px solid #f2f2f2;
}

.tabBox li.current {
  background: #ffffff;
  width: 107.33px;
  height: 43px;
  border-radius: 4px;
  border: 1px solid #f2f2f2;
  padding: 5px;
}

.tabBox li span {
  position: relative;
  top: 0.4px;
}

.tabBox img {
  position: relative;
  width: 13px;
  height: 13px;
  margin-right: 15px;
}
</style>
