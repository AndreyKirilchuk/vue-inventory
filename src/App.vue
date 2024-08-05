<script setup>
import Profile from '@/components/Profile.vue'
import Inventory from '@/components/Inventory.vue'
import Carbon from '@/components/Carbon.vue'
import Changetheme from '@/components/Change-theme.vue'


</script>

<template>
  <div class="container">

      <main>
        <profile />

        <Inventory />
      </main>

      <Carbon />

      <Changetheme/>
  </div>
</template>

<style scoped>
main {
  display: flex;
  gap: 24px;
  margin-bottom: 24px;
}
</style>
