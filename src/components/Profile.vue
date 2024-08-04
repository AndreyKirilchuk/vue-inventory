<script setup>
const stubs = [
  { width: '155px' },
  { width: '100%' },
  { width: '170px' },
  { width: '160px' },
  { width: '140px' }
]
</script>

<template>
  <aside>
    <div>
      <img src="/profile-avatar.png" alt="avatar" class="avatar" />
    </div>

    <div class="name skeleton"></div>

    <div class="info">
      <div class="stub skeleton" v-for="stub in stubs" :style="{ width: stub.width }"></div>
    </div>

    <div class="date skeleton"></div>
  </aside>
</template>

<style scoped>
aside {
  background: #262626;
  padding: 18px 14px;
  border-radius: 12px;
  border: 1px solid #4d4d4d;
}

.avatar {
  border-radius: 8px;
}

.name {
  height: 26px;
  border-radius: 8px;
  margin-top: 20px;
}

.info {
  display: flex;
  flex-direction: column;
  gap: 16px;
  margin: 24px auto;
}

.info .stub {
  height: 10px;
  border-radius: 4px;
  margin: 0 auto;
}

.date {
  width: 80px;
  height: 10px;
  border-radius: 4px;
  margin: 0 auto;
}
</style>
