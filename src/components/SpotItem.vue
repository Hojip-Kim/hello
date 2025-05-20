<template>
  <div class="item">
    <p>지역: {{ item.spotAreaName }}</p>
    <p>관광지명: {{ item.spotName }}</p>
  </div>
</template>

<script setup>
const props = defineProps({
  item: Object,
});
</script>
