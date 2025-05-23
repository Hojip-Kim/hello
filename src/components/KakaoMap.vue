<template>
  <div id="map" style="height: 500px"></div>
</template>

<script setup>
import { onMounted, ref, watch } from 'vue';

const props = defineProps({
  keyword: {
    type: String,
    required: true,
  },
});

// 지도 관련 변수들을 전역 스코프에 선언
let map = null;

let ps = null;

function initMap() {
  var mapContainer = document.getElementById('map');
  var mapOption = {
    center: new kakao.maps.LatLng(37.566826, 126.9786567),
    level: 3,
  };

  // 지도 생성
  map = new kakao.maps.Map(mapContainer, mapOption);

  // 장소 검색 객체 생성
  ps = new kakao.maps.services.Places();

  // 초기 키워드로 검색 실행
  searchPlaces(props.keyword);
}

// 키워드 검색 함수
function searchPlaces(keyword) {
  if (!keyword.trim()) {
    return;
  }

  // 장소검색 객체를 통해 키워드로 장소검색 요청
  ps.keywordSearch(keyword, placesSearchCB);
}

// 키워드 검색 완료 시 호출되는 콜백함수
function placesSearchCB(data, status, pagination) {
  if (status === kakao.maps.services.Status.OK) {
    // 검색된 장소 위치를 기준으로 지도 범위를 재설정하기 위해
    // LatLngBounds 객체에 좌표를 추가합니다
    var bounds = new kakao.maps.LatLngBounds();

    for (var i = 0; i < data.length; i++) {
      displayMarker(data[i]);
      bounds.extend(new kakao.maps.LatLng(data[i].y, data[i].x));
    }

    // 검색된 장소 위치를 기준으로 지도 범위를 재설정합니다
    map.setBounds(bounds);

    // 첫번째 검색 결과의 위치로 중심 이동
    if (data.length > 0) {
      setCenter(data[0].y, data[0].x);
    }
  } else if (status === kakao.maps.services.Status.ZERO_RESULT) {
    console.log('검색 결과가 존재하지 않습니다.');
  } else if (status === kakao.maps.services.Status.ERROR) {
    console.log('검색 중 오류가 발생했습니다.');
  }
}

// 지도 중심을 이동하는 함수
function setCenter(lat, lng) {
  var moveLatLon = new kakao.maps.LatLng(lat, lng);
  map.setCenter(moveLatLon);
}

// 지도에 마커를 표시하는 함수
function displayMarker(place) {
  // 마커를 생성하고 지도에 표시합니다
  var marker = new kakao.maps.Marker({
    map: map,
    position: new kakao.maps.LatLng(place.y, place.x),
  });

  // 마커에 클릭이벤트를 등록합니다
  kakao.maps.event.addListener(marker, 'click', function () {
    // 마커를 클릭하면 장소명이 인포윈도우에 표출됩니다
    infowindow.setContent(
      '<div style="padding:5px;font-size:12px;">' + place.place_name + '</div>'
    );
    infowindow.open(map, marker);
  });
}

onMounted(() => {
  if (window.kakao && window.kakao.maps) {
    initMap();
  } else {
    const script = document.createElement('script');
    script.src = `//dapi.kakao.com/v2/maps/sdk.js?appkey=4471a58e073db9f15a734ac7090a89dc&libraries=services&autoload=false`;
    script.async = true;

    script.onload = () => {
      kakao.maps.load(initMap);
    };

    document.head.appendChild(script);
  }
});

watch(
  () => props.keyword,
  (newKeyword) => {
    if (map && ps && newKeyword) {
      searchPlaces(newKeyword);
    }
  },
  { immediate: true }
);
</script>
