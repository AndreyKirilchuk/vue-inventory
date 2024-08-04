<script setup>
import Profile from '@/components/Profile.vue'
import Inventory from '@/components/Inventory.vue'
import Footer from './components/Carbon.vue'
import Carbon from '@/components/Carbon.vue'
</script>

<template>
  <div class="container">
    <div class="container_inner">
      <main>
        <profile />

        <Inventory />
      </main>

      <Carbon />
    </div>
  </div>
</template>

<style scoped>
main {
  display: flex;
  gap: 24px;
  margin-bottom: 24px;
}
</style>
