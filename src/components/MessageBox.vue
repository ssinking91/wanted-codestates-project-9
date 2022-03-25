<template>
  <div class="message-box">기업 정보가 없습니다</div>
</template>

<script>
export default {
  data() {
    return {};
  },
  method: {},
};
</script>

<style>
.message-box {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
  z-index: 99;
  opacity: 1;
  width: 328px;
  height: 60px;
  background-color: #e34242;
  border-radius: 8px;
  color: #fff;
  font-size: 14px;
  font-weight: 600;
  display: flex;
  justify-content: center;
  align-items: center;

  animation: fadeOut 1.5s;
}
@keyframes fadeOut {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
</style>
