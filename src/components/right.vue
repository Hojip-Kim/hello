<template>
  <div class="right-container">
    <SpotItem
      v-for="item in items"
      :key="item.spotName"
      :item="item"
      @item="setItem"
    ></SpotItem>
  </div>
</template>

<script setup>
import axios from 'axios';
import { ref, watch } from 'vue';
import SpotItem from './spotItem.vue';

const today = new Date();
const yyyy = today.getFullYear();
const mm = String(today.getMonth() + 1).padStart(2, '0');
const dd = String(today.getDate()).padStart(2, '0');
const yyyymmdd = `${yyyy}${mm}${dd}`;

const props = defineProps({
  id: Number,
});

const setItem = (item) => {
  emits('item', item);
};

const emits = defineEmits(['item']);

const items = ref([]);

watch(
  () => props.id,
  async (newVal) => {
    console.log(newVal);
    try {
      const res = await axios.get(
        'https://apis.data.go.kr/1360000/TourStnInfoService1/getTourStnVilageFcst1',
        {
          params: {
            ServiceKey:
              'GFRS31QvZhrKFGKKPPnJ8sev03+tbYneQmBOJYIAWLWegGlYOBds4Cj1ysyo/BuxVIONEx9/7QcDM85+XQPlgg==',
            pageNo: 1,
            numOfRows: 20,
            dataType: 'JSON',
            CURRENT_DATE: yyyymmdd,
            HOUR: '12',
            COURSE_ID: newVal,
          },
        }
      );
      if (res.data) {
        items.value = Array.from(
          new Map(
            res.data.response.body.items.item.map((obj) => [obj.spotName, obj])
          ).values()
        );
      } else items.value = '';
    } catch (err) {
      alert('에러 발생');
    }
  }
);
</script>
