<script setup>
defineProps({
  modalActive: Boolean,
  img: String,
  quantity: Number
})

const emitEvent = defineEmits(['closeModal', 'deleteItem'])
</script>

<template>
  <div class="fon" :class="{ active: modalActive }" @click="emitEvent('closeModal')"></div>

  <div class="modal_container" :class="{ active: modalActive }">
    <div class="cross">
      <img src="/cross.svg" alt="cross" @click="emitEvent('closeModal')" />
    </div>

    <div class="item_img">
      <img :src="img" :alt="img" />
    </div>

    <div class="name skeleton"></div>

    <div class="info">
      <div class="stub skeleton" v-for="stub in stubs" :style="{ width: stub.width }"></div>
    </div>

    <div class="date skeleton"></div>
  </div>
</template>

<style scoped>
.fon {
  display: none;
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  transition: all 0.3s ease-in-out;
  z-index: 1;
  background: inherit;
}

.fon.active {
  display: block;
}

.modal_container {
  right: -250px;
  position: absolute;

  width: 250px;
  height: 100%;
  background: rgba(38, 38, 38, 0.5);
  backdrop-filter: blur(30px);
  transition: all 0.3s ease-in-out;
  border-left: 1px solid #4d4d4d;
  z-index: 100;
}

.modal_container.active {
  right: 0;
}

.cross {
  position: absolute;
  top: 8px;
  right: 8px;
}

.item_img {
}
</style>
