<template>
  <div @click="() => emits('id', course.id)">
    <p>{{ course.id }} : {{ course.name }}</p>
  </div>
</template>

<script setup>
const props = defineProps({
  course: Object,
});
const emits = defineEmits(["id"]);
</script>

<style scoped>
div {
  @apply cursor-pointer p-4 border border-gray-300 rounded-xl shadow-sm hover:shadow-md hover:border-blue-500 transition duration-200 bg-white;
}
p {
  @apply text-lg font-semibold text-gray-800;
}
</style>
