<script setup>
import BaseButton from './components/BaseButton.vue';
import LeftSide from './components/CourseList.vue';
import Modal from './components/Modal.vue';
import RightSide from './components/right.vue';

import { ref, watch } from 'vue';

const isModalOpen = ref(false);

const getId = (id) => {
  setId.value = id;
};

const setId = ref(0);

const tmpData = ref({
  name: '남호고택에서의 하룻밤',
  region: '충청남도 천안시',
  temperature: 20,
});

const openModal = (item) => {
  isModalOpen.value = true;
  tmpData.value = item;
};

const closeModal = () => {
  isModalOpen.value = false;
};
</script>

<template>
  <div @click="openModal"></div>
  <div class="container">
    <LeftSide @id="getId" />
    <RightSide :id="setId" @item="(item) => openModal(item)" />

    <Modal
      :is-open="isModalOpen"
      :content="tmpData"
      @close-modal="closeModal"
    />
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-flow: row wrap;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 100vh;
}
</style>
