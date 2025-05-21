<template>
  <div class="course-item" @click="() => emits('id', course.id)">
    <div class="course-id">{{ course.id }}</div>
    <div class="course-content">
      <h3 class="course-name">{{ course.name }}</h3>
    </div>
    <div class="course-arrow">
      <svg
        width="16"
        height="16"
        viewBox="0 0 16 16"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M6 12L10 8L6 4"
          stroke="currentColor"
          stroke-width="1.5"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  course: Object,
});
const emits = defineEmits(['id']);
</script>

<style scoped>
.course-item {
  display: flex;
  align-items: center;
  flex-direction: column;
  padding: 16px;
  background-color: white;
  border-radius: 16px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
  cursor: pointer;
  transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
  width: 30%;
}

.course-item::after {
  content: '';

  inset: 0;
  border-radius: 16px;
  box-shadow: 0 0 0 0 rgba(0, 0, 0, 0);
  transition: box-shadow 0.2s ease;
}

.course-item:hover {
  transform: translateY(-2px);
}

.course-item:hover::after {
  box-shadow: 0 10px 20px -5px rgba(0, 0, 0, 0.08);
}

.course-id {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 32px;
  height: 32px;
  background-color: #eef2ff;
  color: #4f46e5;
  font-weight: 600;
  font-size: 14px;
  border-radius: 50%;
  margin-right: 12px;
  flex-shrink: 0;
}

.course-content {
  flex: 1;
  margin-right: 12px;
}

.course-name {
  font-size: 15px;
  font-weight: 600;
  color: #333;
  margin-bottom: 4px;
  transition: color 0.2s ease;
}

.course-item:hover .course-name {
  color: #4f46e5;
}

.course-badge {
  display: inline-block;
  background-color: #f3f4f6;
  color: #6b7280;
  font-size: 11px;
  font-weight: 500;
  padding: 2px 8px;
  border-radius: 8px;
  line-height: 1.5;
}

.course-arrow {
  color: #9ca3af;
  transition: transform 0.2s ease, color 0.2s ease;
}

.course-item:hover .course-arrow {
  transform: translateX(2px);
  color: #4f46e5;
}
</style>
