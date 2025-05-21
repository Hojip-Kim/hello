<template>
  <div class="left-container">
    <CourseItem
      v-for="course in courses"
      :key="course.id"
      :course="course"
      @id="handleId"
    ></CourseItem>
  </div>
</template>

<script setup>
import CourseItem from './CourseItem.vue';
import courses from '../assets/data';
import { ref } from 'vue';

const emits = defineEmits(['id']);

const handleId = (id) => {
  console.log('CourseList received id:', id);
  emits('id', id);
};
</script>

<style scoped>
.left-container {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  gap: 16px;
  flex-wrap: wrap;
  height: 30%;
  overflow-y: scroll;
  padding-top: 20px;
  border-radius: 20px;
  padding: 20px;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2);

  margin: 20px 50px 50px 50px;
}
</style>
