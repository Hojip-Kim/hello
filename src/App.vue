<script setup>
import BaseButton from './components/BaseButton.vue';
import LeftSide from './components/CourseList.vue';
import Modal from './components/Modal.vue';
import RightSide from './components/right.vue';
import Header from './components/Header.vue';
import { ref, watch } from 'vue';
import KakaoMap from './components/KakaoMap.vue';
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

const keyword = ref('가산디지털단지');

const setMapInfo = (item) => {
  keyword.value = item.spotName;
};

const closeModal = () => {
  isModalOpen.value = false;
};
</script>

<template>
  <div @click="openModal"></div>
  <div class="container">
    <Header />

    <LeftSide @id="getId" />

    <KakaoMap
      :keyword="keyword"
      style="
        margin: 0px 50px 50px 50px;
        box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2);
        border-radius: 20px;
      "
    />
    <RightSide
      :id="setId"
      @item="
        (item) => {
          openModal(item);
          setMapInfo(item);
        }
      "
    />

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
  flex-direction: column;
  justify-content: space-between;
  box-sizing: border-box;
  width: 100%;
  height: 100vh;

  background-color: #f0f0f0;
}
</style>
