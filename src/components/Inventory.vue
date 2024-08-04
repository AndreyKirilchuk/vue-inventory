<script setup>
import Box from '@/components/Box.vue'
import Modal from '@/components/Modal.vue'
import { reactive, ref } from 'vue'

const items = reactive([
  {
    id: 1,
    img: '/item1.svg',
    quantity: 4
  },
  {
    id: 2,
    img: '/item2.svg',
    quantity: 2
  },
  {
    id: 3,
    img: '/item3.svg',
    quantity: 5
  },
  {
    id: 4,
    img: '',
    quantity: 0
  },
  {
    id: 5,
    img: '',
    quantity: 0
  },
  {
    id: 6,
    img: '',
    quantity: 0
  },
  {
    id: 7,
    img: '',
    quantity: 0
  },
  {
    id: 8,
    img: '',
    quantity: 0
  },
  {
    id: 9,
    img: '',
    quantity: 0
  },
  {
    id: 10,
    img: '',
    quantity: 0
  },
  {
    id: 11,
    img: '',
    quantity: 0
  },
  {
    id: 12,
    img: '',
    quantity: 0
  },
  {
    id: 13,
    img: '',
    quantity: 0
  },
  {
    id: 14,
    img: '',
    quantity: 0
  },
  {
    id: 15,
    img: '',
    quantity: 0
  },
  {
    id: 16,
    img: '',
    quantity: 0
  },
  {
    id: 17,
    img: '',
    quantity: 0
  },
  {
    id: 18,
    img: '',
    quantity: 0
  },
  {
    id: 19,
    img: '',
    quantity: 0
  },
  {
    id: 20,
    img: '',
    quantity: 0
  },
  {
    id: 21,
    img: '',
    quantity: 0
  },
  {
    id: 22,
    img: '',
    quantity: 0
  },
  {
    id: 23,
    img: '',
    quantity: 0
  },
  {
    id: 24,
    img: '',
    quantity: 0
  },
  {
    id: 25,
    img: '',
    quantity: 0
  }
])

const modalActive = ref(false)
const itemModal = ref({ id: '1', img: '/item1.svg', quantity: 1 })

const onDropItem = (draggedId, targetId) => {
  const draggedItem = items.find((item) => item.id === Number(draggedId))
  const targetItem = items.find((item) => item.id === Number(targetId))

  if (draggedItem && targetItem) {
    ;[draggedItem.img, targetItem.img] = [targetItem.img, draggedItem.img]
    ;[draggedItem.quantity, targetItem.quantity] = [targetItem.quantity, draggedItem.quantity]
  }
}

const openModal = (id) => {
  modalActive.value = true
  itemModal.value = items.find((item) => item.id === id)
}

const closeModal = () => {
  modalActive.value = false
  itemModal.value = ''
}

const deleteItem = (id, qunatityRemove) => {
  itemModal.quantity - qunatityRemove
  if (itemModal.quantity === 0) {
    itemModal.img = ''
  }
}
</script>

<template>
  <section class="inventory_container">
    <Box
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :img="item.img"
      :quantity="item.quantity"
      @dropItem="onDropItem"
      @openModal="openModal"
    />

    <Modal
      :modalActive="modalActive"
      :img="itemModal.img"
      :quantity="itemModal.quantity"
      @deleteItem="deleteItem"
      @closeModal="closeModal"
    />
  </section>
</template>

<style scoped>
.inventory_container {
  border-radius: 12px;
  width: 100%;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  border: 1px solid #4d4d4d;
  position: relative;
  overflow: hidden;
}
</style>
