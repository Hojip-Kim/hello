<template>
  <div>
    <CourseItem
      v-for="course in courses"
      :key="course.id"
      :course="course"
      @id="() => emits('id', course.id)"
    ></CourseItem>
  </div>
</template>

<script setup>
import CourseItem from "./CourseItem.vue";
import courses from "../assets/data";

const emits = defineEmits(["id"]);
</script>

<style scoped>
div {
  @apply max-w-md mt-10 space-y-4;
}
</style>
