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

        <div class="modal-title">
          <h2>관광지 정보</h2>
        </div>

        <div class="modal-cards">
          <!-- 기본 정보 카드 -->
          <div class="info-card">
            <div class="info-card-header">
              <svg
                class="info-icon"
                width="20"
                height="20"
                viewBox="0 0 20 20"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M10.0001 3.33337C8.16082 3.33337 6.66675 4.82743 6.66675 6.66671C6.66675 8.50599 8.16082 10 10.0001 10C11.8394 10 13.3334 8.50599 13.3334 6.66671C13.3334 4.82743 11.8394 3.33337 10.0001 3.33337Z"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
                <path
                  d="M5 16.6667C5 13.9053 7.2386 11.6667 10 11.6667C12.7614 11.6667 15 13.9053 15 16.6667"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
              </svg>
              <h3>기본 정보</h3>
            </div>
            <div class="info-card-content">
              <div class="info-row">
                <span class="info-label">관광지명</span>
                <span class="info-value">{{
                  props.content.spotName || '-'
                }}</span>
              </div>
              <div class="info-row">
                <span class="info-label">지역</span>
                <span class="info-value">{{
                  props.content.spotAreaName || '-'
                }}</span>
              </div>
            </div>
          </div>

          <!-- 날씨 정보 카드 -->
          <div class="info-card">
            <div class="info-card-header">
              <svg
                class="info-icon"
                width="20"
                height="20"
                viewBox="0 0 20 20"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M10 3.33337V5.00004"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
                <path
                  d="M10 15V16.6667"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
                <path
                  d="M4.1084 4.10833L5.2834 5.28333"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
                <path
                  d="M14.7166 14.7167L15.8916 15.8917"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
                <path
                  d="M3.33325 10H4.99992"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
                <path
                  d="M15 10H16.6667"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
                <path
                  d="M4.1084 15.8917L5.2834 14.7167"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
                <path
                  d="M14.7166 5.28333L15.8916 4.10833"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
                <path
                  d="M10 13.3334C11.8409 13.3334 13.3333 11.8409 13.3333 10.0001C13.3333 8.15913 11.8409 6.66669 10 6.66669C8.15906 6.66669 6.66663 8.15913 6.66663 10.0001C6.66663 11.8409 8.15906 13.3334 10 13.3334Z"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
              </svg>
              <h3>날씨 정보</h3>
            </div>
            <div class="info-card-content">
              <div class="weather-grid">
                <div class="weather-item">
                  <span class="weather-label">습도</span>
                  <span class="weather-value temperature"
                    >{{ props.content.rhm || '-' }}%</span
                  >
                </div>
                <div class="weather-item">
                  <span class="weather-label">현재 기온</span>
                  <span class="weather-value temperature"
                    >{{ props.content.th3 || '-' }}℃</span
                  >
                </div>
                <div class="weather-item">
                  <span class="weather-label">하늘 상태</span>
                  <span class="weather-value">{{
                    props.content.sky || '-'
                  }}</span>
                </div>
                <div class="weather-item">
                  <span class="weather-label">강수 확률</span>
                  <span class="weather-value"
                    >{{ props.content.pop || '-' }}%</span
                  >
                </div>
              </div>
            </div>
          </div>

          <!-- 바람 정보 카드 -->
          <div class="info-card" v-if="props.content.wd || props.content.ws">
            <div class="info-card-header">
              <svg
                class="info-icon"
                width="20"
                height="20"
                viewBox="0 0 20 20"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M2.5 10H9.16667C10.0871 10 10.8333 9.25381 10.8333 8.33333C10.8333 7.41286 10.0871 6.66667 9.16667 6.66667C8.24619 6.66667 7.5 7.41286 7.5 8.33333"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
                <path
                  d="M2.5 15H13.3333C14.2538 15 15 14.2538 15 13.3333C15 12.4129 14.2538 11.6667 13.3333 11.6667C12.4129 11.6667 11.6667 12.4129 11.6667 13.3333"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
                <path
                  d="M2.5 5H15.8333C16.7538 5 17.5 5.74619 17.5 6.66667C17.5 7.58714 16.7538 8.33333 15.8333 8.33333C14.9129 8.33333 14.1667 7.58714 14.1667 6.66667"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
              </svg>
              <h3>바람 정보</h3>
            </div>
            <div class="info-card-content">
              <div class="info-row">
                <span class="info-label">풍향</span>
                <span class="info-value">{{ wd || '-' }}</span>
              </div>
              <div class="info-row">
                <span class="info-label">풍속</span>
                <span class="info-value"
                  >{{ props.content.ws || '-' }} m/s</span
                >
              </div>
            </div>
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
  padding: 16px;
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
  width: 100%;
  max-width: 480px;
  background-color: white;
  border-radius: 24px;
  padding: 24px;
  display: flex;
  flex-direction: column;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  animation: modal-appear 0.3s ease-out forwards;
  max-height: 90vh;
  overflow-y: auto;
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
  margin-bottom: 8px;
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

.modal-title {
  margin-bottom: 20px;
}

.modal-title h2 {
  font-size: 20px;
  font-weight: 700;
  color: #111827;
}

.modal-cards {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.info-card {
  background-color: #f9fafb;
  border-radius: 16px;
  overflow: hidden;
  transition: transform 0.2s, box-shadow 0.2s;
}

.info-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}

.info-card-header {
  padding: 16px;
  border-bottom: 1px solid #f3f4f6;
  display: flex;
  align-items: center;
  gap: 10px;
}

.info-card-header h3 {
  font-size: 16px;
  font-weight: 600;
  color: #374151;
  margin: 0;
}

.info-icon {
  color: #4f46e5;
}

.info-card-content {
  padding: 16px;
}

.info-row {
  display: flex;
  justify-content: space-between;
  margin-bottom: 12px;
}

.info-row:last-child {
  margin-bottom: 0;
}

.info-label {
  font-size: 14px;
  color: #6b7280;
  font-weight: 500;
}

.info-value {
  font-size: 14px;
  color: #111827;
  font-weight: 600;
}

.weather-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
}

.weather-item {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.weather-label {
  font-size: 12px;
  color: #6b7280;
  font-weight: 500;
}

.weather-value {
  font-size: 16px;
  color: #111827;
  font-weight: 600;
}

.weather-value.temperature {
  color: #ef4444;
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

let wd;

if (props.content.wd == 0) {
  wd = '북풍';
} else if (props.content.wd > 0 && props.content.wd < 90) {
  wd = '북동풍';
} else if (props.content.wd == 90) {
  wd = '동풍';
} else if (props.content.wd > 90 && props.content.wd < 180) {
  wd = '남동풍';
} else if (props.content.wd == 180) {
  wd = '남풍';
} else if (props.content.wd > 180 && props.content.wd < 270) {
  wd = '남서풍';
} else if (props.content.wd == 270) {
  wd = '서풍';
} else if (props.content.wd > 270 && props.content.wd < 360) {
  wd = '북서풍';
} else {
  wd = '-';
}

const emit = defineEmits(['closeModal']);

const closeModal = () => {
  emit('closeModal');
};
</script>
