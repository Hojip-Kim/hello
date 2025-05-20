<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  id: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <div class="button-container" :id="props.id">
    {{ props.name }}
  </div>
</template>

<style scoped>
.button-container {
  @apply bg-blue-500 text-white px-4 py-2 rounded-md;
}
</style>
