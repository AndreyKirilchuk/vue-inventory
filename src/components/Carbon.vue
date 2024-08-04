<script setup></script>

<template>
  <div class="carbon">
    <div class="carbon_inner skeleton"></div>

    <div class="cross">
      <img src="/cross.svg" alt="close_carbon" width="24px" />
    </div>
  </div>
</template>

<style scoped>
.carbon {
  background: #262626;
  padding: 18px 14px;
  border-radius: 12px;
  border: 1px solid #4d4d4d;
  width: 100%;
  padding: 18px 60px 18px 18px;
  position: relative;
}

.cross {
  position: absolute;
  top: 8px;
  right: 8px;
  cursor: pointer;
}

.carbon_inner {
  width: 100%;
  height: 36px;
  border-radius: 12px;
}

.sceleton {
  background: linear-gradient(to right, #3c3c3c, #444444, #333333);
  background-size: 200% 100%;
  animation: gradientAnimation 10s ease infinite;
}

@keyframes gradientAnimation {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>
