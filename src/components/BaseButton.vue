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
  variant: {
    type: String,
    default: 'primary',
    validator: (value) => ['primary', 'secondary', 'tertiary'].includes(value),
  },
  size: {
    type: String,
    default: 'medium',
    validator: (value) => ['small', 'medium', 'large'].includes(value),
  },
});
</script>

<template>
  <button
    class="button"
    :class="[`button-${props.variant}`, `button-${props.size}`]"
    :id="props.id"
  >
    <span class="button-text">{{ props.name }}</span>
  </button>
</template>

<style scoped>
.button {
  @apply inline-flex items-center justify-center rounded-md font-medium transition-all focus:outline-none;
  transform: translateZ(0);
  will-change: transform;
}

.button:active {
  @apply transform scale-[0.98];
}

.button-primary {
  @apply bg-blue-500 text-white shadow-sm hover:bg-blue-600 active:bg-blue-700;
}

.button-secondary {
  @apply bg-gray-100 text-gray-800 shadow-sm hover:bg-gray-200 active:bg-gray-300;
}

.button-tertiary {
  @apply bg-white text-gray-800 border border-gray-300 shadow-sm hover:bg-gray-50 active:bg-gray-100;
}

.button-small {
  @apply text-sm px-3 py-1.5 rounded-md;
}

.button-medium {
  @apply text-sm px-4 py-2 rounded-md;
}

.button-large {
  @apply text-base px-5 py-2.5 rounded-lg;
}

.button-text {
  @apply leading-tight;
}
</style>
