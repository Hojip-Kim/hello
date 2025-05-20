<template>
  <div class="spot-item" @click="() => emits('item', item)">
    <div class="spot-item-content">
      <div class="spot-item-header">
        <div class="spot-name">{{ item.spotName }}</div>
        <div class="area-tag">{{ item.spotAreaName }}</div>
      </div>
      <div class="spot-details">
        <div class="detail-item" v-if="item.th3">
          <svg class="icon" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M8 3V13" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M12 7C12 5.34315 10.2091 4 8 4C5.79086 4 4 5.34315 4 7C4 8.65685 5.79086 10 8 10C8.35292 10 8.69504 9.9626 9.01449 9.89253C10.0181 9.68066 12 8.6934 12 7Z" stroke="currentColor" stroke-width="1.5"/>
          </svg>
          <span>{{ item.th3 }}℃</span>
        </div>
        <div class="detail-item" v-if="item.sky">
          <svg class="icon" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M4.5 7.5C4.5 5.84315 5.84315 4.5 7.5 4.5C9.15685 4.5 10.5 5.84315 10.5 7.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M2.5 9.5C2.5 8.11929 3.61929 7 5 7C6.38071 7 7.5 8.11929 7.5 9.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M8.5 9.5C8.5 8.11929 9.61929 7 11 7C12.3807 7 13.5 8.11929 13.5 9.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M2.5 9.5L13.5 9.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M4 12L5 10.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M8 12L9 10.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M12 12L13 10.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span>{{ item.sky }}</span>
        </div>
        <div class="detail-item" v-if="item.pop">
          <svg class="icon" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M7 4L5 8" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M11 4L9 8" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M9 11L7 15" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M13 11L11 15" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span>{{ item.pop }}%</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const emits = defineEmits(['item']);

const props = defineProps({
  item: Object,
});
</script>

<style scoped>
.spot-item {
  background-color: white;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
  transition: all 0.2s ease;
  cursor: pointer;
  transform: translateZ(0);
  will-change: transform;
}

.spot-item:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 20px rgba(0, 0, 0, 0.08);
}

.spot-item:active {
  transform: translateY(-2px);
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.06);
}

.spot-item-content {
  padding: 16px;
}

.spot-item-header {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 12px;
}

.spot-name {
  font-size: 16px;
  font-weight: 600;
  color: #333;
}

.area-tag {
  display: inline-block;
  background-color: #f3f4f6;
  border-radius: 12px;
  padding: 4px 10px;
  font-size: 12px;
  font-weight: 500;
  color: #4b5563;
  align-self: flex-start;
}

.spot-details {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}

.detail-item {
  display: flex;
  align-items: center;
  gap: 6px;
  background-color: #f9fafb;
  border-radius: 8px;
  padding: 6px 10px;
  font-size: 13px;
  color: #374151;
  font-weight: 500;
}

.icon {
  color: #6b7280;
}
</style>
