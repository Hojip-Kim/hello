<template>
  <div>
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
div {
  @apply max-w-md mt-10 space-y-4;
}
</style>
