<script setup>
const props = defineProps({
  id: Number,
  img: String,
  quantity: Number
})

const emitEvent = defineEmits(['onDropItem', 'openModal'])

const onDragStart = (event) => {
  event.dataTransfer.setData('text/plain', props.id)
}

const onDrop = (event) => {
  const draggedId = event.dataTransfer.getData('text/plain')
  emitEvent('dropItem', draggedId, props.id)
  event.dataTransfer.clearData()
}

const openModal = (id) => {
  if(props.img && props.quantity > 0){
    emitEvent('openModal', id)
  }
}
</script>

<template>
  <div
    class="box"
    :draggable="img && quantity > 0"
    @dragstart="onDragStart"
    @dragover.prevent
    @drop="onDrop"
    :class="{'box-hover': img && quantity > 0}"
    @click="openModal(id)"
  >
    <img
      :src="img"
      :alt="img"
      width="54px"
      v-if="img"
      draggable="false"
    />

    <div class="quantity_container" v-if="quantity">
      {{ quantity }}
    </div>
  </div>
</template>

<style scoped>
.box {
  border: 1px solid var(--var--elborder);
  background-color: var(--var--elbackground);
  position: relative;
  transition: 0.3s;
}

.box-hover{
  cursor: pointer;
}

.box-hover:hover{
  background: var(--var--hoverbackground);
}

.dragging {
  border-radius: 24px !important;
}

.box img {
  position: absolute;
  transform: translate(50%, 50%);
}

.box:nth-child(1) {
  border-top-left-radius: 12px;
}

.box:nth-child(5) {
  border-top-right-radius: 12px;
}

.box:nth-child(21) {
  border-bottom-left-radius: 12px;
}

.box:nth-child(25) {
  border-bottom-right-radius: 12px;
}

.quantity_container {
  position: absolute;
  right: 0;
  bottom: 0;
  border-top-left-radius: 6px;
  border-left: 2px solid var(--var--elborder);
  border-top: 2px solid var(--var--elborder);
  width: 16px;
  height: 16px;
  display: flex;
  justify-content: center;
  font-size: 10px;
  color: var(--var--boxcolor);
}
</style>
