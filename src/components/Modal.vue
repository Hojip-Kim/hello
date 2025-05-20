<template>
  <div class="modal-container" v-if="props.isOpen" @click="closeModal">
    <div class="modal-box" @click.stop>
      <div class="modal-close-container">
        <span class="modal-close" @click="closeModal">X</span>
      </div>
      <div class="modal-header">
        <div class="modal-header-name">
          <span>이름</span>
          <span>{{ props.content.name }}</span>
        </div>
        <div class="modal-header-region">
          <span>지역</span>
          <span>{{ props.content.region }}</span>
        </div>
      </div>
      <div class="modal-content">
        <div class="modal-content-temperature">
          <span>온도</span>
          <span>{{ props.content.temperature }}℃</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);

  z-index: 1000;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-box {
  width: 700px;
  height: 300px;
  background-color: white;
  border-radius: 10px;
  padding: 10px;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.8);

  opacity: 1;
}

.modal-close-container {
  width: 100%;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.modal-close {
  top: 10px;
  right: 10px;
  font-size: 1.2rem;
  font-weight: bold;
  color: #000;
  font-family: 'Pretendard', sans-serif;
  cursor: pointer;
}

.modal-header {
  width: 100%;
  height: 20%;

  display: flex;
  justify-content: space-between;
  align-items: center;

  padding: 0px 0px 20px 0px;
}

.modal-header-name {
  width: 100%;
  height: 100%;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-right: 1px solid gray;
}

.modal-header-name span:first-child {
  font-size: 1.4rem;
  font-weight: bold;
  color: #000;
  font-family: 'Pretendard', sans-serif;
}

.modal-header-region {
  width: 100%;
  height: 100%;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.modal-header-region span:first-child {
  font-size: 1.4rem;
  font-weight: bold;
  color: #000;
  font-family: 'Pretendard', sans-serif;
}

.modal-header span {
  font-size: 1.1rem;
  font-weight: bold;
  color: #000;
  font-family: 'Pretendard', sans-serif;
}

.modal-content {
  width: 100%;
  height: 80%;
  border: 1px solid gray;
  border-radius: 10px;
  box-shadow: inset 0 0 5px 0px rgba(0, 0, 0, 0.3);

  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content-temperature {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.modal-content-temperature span:first-child {
  font-size: 1.4rem;
  font-weight: bold;
  color: #000;
  font-family: 'Pretendard', sans-serif;
}

.modal-content-temperature span:last-child {
  font-size: 1.2rem;
  font-weight: bold;
  color: #000;
  font-family: 'Pretendard', sans-serif;
}
</style>
<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false,
  },
  content: {
    name: {
      type: String,
      default: '',
    },
    temperature: {
      type: Number,
      default: 0,
    },
    region: {
      type: String,
      default: '',
    },
  },
});

const emit = defineEmits(['closeModal']);

const closeModal = () => {
  emit('closeModal');
};
</script>
