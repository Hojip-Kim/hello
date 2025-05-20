<script setup>
import BaseButton from './components/BaseButton.vue';
import LeftSide from './components/CourseList.vue';
import Modal from './components/Modal.vue';
import RightSide from './components/right.vue';
import { hardcodedData } from './hardcoding';

import { ref, watch } from 'vue';

const isModalOpen = ref(false);

const id = ref(1);

const tmpData = ref({
  name: '남호고택에서의 하룻밤',
  region: '충청남도 천안시',
  temperature: 20,
});

const openModal = () => {
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};
</script>

<template>
  <div @click="openModal">hello</div>
  <div class="container">
    <LeftSide :hardcoded-data="hardcodedData" @id="id" />
    <RightSide :id="id" />

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
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 100vh;
}
</style>
