<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  modalActive: Boolean,
  img: String,
  itemQuantity: Number
})

const quantity = ref()

const stubs = [
  { width: '100%' },
  { width: '100%' },
  { width: '100%' },
  { width: '180px' },
  { width: '80px' }
]

const emitEvent = defineEmits(['closeModal', 'deleteItem'])

const deleteActive = ref(false)
const error = ref(false)

const openDelete = () => {
  deleteActive.value = true
}

const closeDelete = () => {
  deleteActive.value = false
}

const closeModal = () => {
  emitEvent('closeModal')
  closeDelete()
}

const errorAnimate = () => {
  error.value = false
  setTimeout(() => {
    error.value = true
  }, 0.01)
}

const deleteItem = () => {
  if (quantity.value !== undefined && quantity.value > 0) {
    if (quantity.value <= props.itemQuantity) {
      emitEvent('deleteItem', quantity.value)
      quantity.value = null
      closeDelete()
    } else {
      errorAnimate()
    }
  } else {
    errorAnimate()
  }
}

const applyInput = () => {
  error.value = false
}
</script>

<template>
  <div class="fon" :class="{ active: modalActive }" @click="closeModal"></div>

  <div class="modal_container" :class="{ active: modalActive }">
    <div class="cross">
      <img src="/cross.svg" alt="cross" @click="emitEvent('closeModal')" />
    </div>

    <div class="item_img">
      <img :src="img" :alt="img" width="130px" />
    </div>

    <div class="name skeleton"></div>

    <div class="info">
      <div class="stub skeleton" v-for="stub in stubs" :style="{ width: stub.width }"></div>
    </div>

    <hr />

    <button class="delete-btn" @click="openDelete">Удалить предмет</button>

    <div class="delete_fon" :class="{ active: deleteActive }" @click="closeDelete"></div>
    <form class="delete_container" :class="{ active: deleteActive }" @submit.prevent="deleteItem">
      <input
        type="number"
        placeholder="Введите количество"
        v-model="quantity"
        :class="{ error: error }"
        @input="applyInput"
      />

      <div class="delete_inner">
        <button class="cancel-btn" @click="closeDelete" type="button">Отмена</button>

        <button class="delete-btn" type="submit">Подтвердить</button>
      </div>
    </form>
  </div>
</template>

<style scoped>
.fon,
.delete_fon {
  display: none;
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  transition: all 0.3s ease-in-out;
  z-index: 1;
  background: inherit;
  opacity: 0;
}

.fon.active,
.delete_fon.active {
  display: block;
}

.modal_container {
  right: -250px;
  position: absolute;
  width: 250px;
  height: 100%;
  background: var(--var--modalbackground);
  backdrop-filter: blur(30px);
  transition: all 0.3s ease-in-out;
  border-left: 1px solid var(--var--elborder);
  z-index: 100;
  padding: 15px 18px;
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
  height: 43%;
  padding: 30px 45px;
  display: flex;
  justify-content: center;
  border-bottom: 1px solid var(--var--elborder);
}

hr {
  border: 1px solid var(--var--elborder);
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

.delete-btn {
  background: #fa7272;
  color: white;
  padding: 11px 0px;
}

button {
  width: 100%;
  border: 0;
  padding: 8px 0px;
  border-radius: 8px;
  cursor: pointer;
  margin-top: 10px;
  font-size: 14px;
}

.delete_container {
  padding: 20px;
  width: 100%;
  position: absolute;
  margin-bottom: 20px;
  bottom: -150px;
  transition: 0.3s;
  background: var(--var--elbackground);
  left: 0;
  border-top: 1px solid var(--var--elborder);
  z-index: 100;
}

.delete_container.active {
  bottom: -18px;
}

input {
  padding: 12px;
  box-sizing: border-box;
  border: 1px solid var(--var--elborder);
  border-radius: 4px;
  background: var(--var--elbackground);
  outline: none;
  color: var(--var--boxcolor);
  font-weight: 500;
  width: 100%;
}

.delete_inner {
  display: flex;
  gap: 10px;
}

.delete_inner button {
  box-shadow: 0 0 10px rgba(255, 107, 107, 0.7);
  padding: 8px 15px;
}

.error {
  border: 1px solid #fa7272 !important;
  animation: shake 0.5s;
}

@keyframes shake {
  0% {
    transform: translateY(2px);
  }
  25% {
    transform: translateY(-4px);
  }
  50% {
    transform: translateY(3px);
  }
  75% {
    transform: translateY(-2px);
  }
  100% {
    transform: translateY(0);
  }
}
</style>
