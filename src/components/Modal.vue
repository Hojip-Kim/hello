<template>
  <transition name="modal-fade">
    <div class="modal-container" v-if="props.isOpen" @click="closeModal">
      <div class="modal-box" @click.stop>
        <div class="modal-close-container">
          <div class="modal-close" @click="closeModal">
            <svg
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M18 6L6 18"
                stroke="#333333"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
              <path
                d="M6 6L18 18"
                stroke="#333333"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </div>
        </div>
        <div class="modal-header">
          <div class="modal-header-name">
            <span class="label">이름</span>
            <span class="value">{{ props.content.name }}</span>
          </div>
          <div class="modal-header-region">
            <span class="label">지역</span>
            <span class="value">{{ props.content.region }}</span>
          </div>
        </div>
        <div class="modal-content">
          <div class="modal-content-temperature">
            <span class="label">온도</span>
            <span class="value">{{ props.content.temperature }}℃</span>
          </div>
        </div>
      </div>
    </div>
  </transition>
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

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
  transform: translateY(20px);
}

.modal-box {
  width: 90%;
  max-width: 420px;
  background-color: white;
  border-radius: 24px;
  padding: 24px;
  display: flex;
  flex-direction: column;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  animation: modal-appear 0.3s ease-out forwards;
}

@keyframes modal-appear {
  0% {
    transform: scale(0.95);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

.modal-close-container {
  width: 100%;
  display: flex;
  justify-content: flex-end;
  margin-bottom: 12px;
}

.modal-close {
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  cursor: pointer;
  transition: background-color 0.2s;
}

.modal-close:hover {
  background-color: #f2f4f6;
}

.modal-header {
  width: 100%;
  display: flex;
  gap: 16px;
  margin-bottom: 20px;
}

.modal-header-name,
.modal-header-region {
  flex: 1;
  padding: 16px;
  background-color: #f9fafb;
  border-radius: 16px;
  display: flex;
  flex-direction: column;
  transition: transform 0.2s, box-shadow 0.2s;
}

.modal-header-name:hover,
.modal-header-region:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}

.label {
  font-size: 14px;
  color: #8b95a1;
  margin-bottom: 8px;
  font-weight: 500;
}

.value {
  font-size: 18px;
  color: #333;
  font-weight: 600;
}

.modal-content {
  width: 100%;
  border-radius: 16px;
  background-color: #f9fafb;
  overflow: hidden;
  transition: transform 0.3s, box-shadow 0.3s;
}

.modal-content:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}

.modal-content-temperature {
  width: 100%;
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.modal-content-temperature .value {
  font-size: 32px;
  margin-top: 12px;
  color: #3182f6;
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
    type: Object,
    default: () => ({}),
  },
});

const emit = defineEmits(['closeModal']);

const closeModal = () => {
  emit('closeModal');
};
</script>
