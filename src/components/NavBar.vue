<template>
  <section class="NavBarBox">
    <div class="leftBox">
      <svg
        width="28"
        height="28"
        viewBox="0 0 28 28"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <rect
          x="1"
          y="1"
          width="26"
          height="26"
          rx="13"
          fill="white"
          stroke="#121212"
          stroke-width="2"
        />
        <path
          d="M14 9L9 14L14 19.0001"
          stroke="#121212"
          stroke-width="2"
          stroke-linecap="round"
        />
        <path
          d="M9.35706 14.0001H19"
          stroke="#121212"
          stroke-width="2"
          stroke-linecap="round"
        />
      </svg>
      <p>진단결과</p>
    </div>
    <div class="rightBox">
      <p @click="refresh">다시 진단하기</p>
    </div>
  </section>
</template>

<script>
export default {
  methods: {
    refresh() {
      location.reload();
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

.NavBarBox {
  width: 100%;
  height: 72px;
  display: flex;
}

.leftBox {
  width: 50%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding: 0 16px;
}

.leftBox > svg {
  cursor: pointer;
}

.leftBox > p {
  font-size: 24px;
  font-weight: bold;
  color: #121212;
  margin-left: 12px;
  padding-top: 2px;
}

.rightBox {
  width: 50%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding: 0 16px;
}

.rightBox > p {
  cursor: pointer;
  font-size: 16px;
  color: #6e3cf9;
}
</style>
