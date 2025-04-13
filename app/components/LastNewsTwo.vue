<script setup>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Navigation, Pagination, Autoplay } from 'swiper/modules';
defineProps({ slides: { type: Array, required: true } });

import 'swiper/css';

const pagination = {
  clickable: true,
  renderBullet: function (index, className) {
    return `<span class="${className}" onmouseenter="this.click()">${index + 1}</span>`;
  },
};
</script>

<template>
  <div class="col-4">
    <Swiper
      :modules="[Navigation, Pagination, Autoplay]"
      :slides-per-view="1"
      :space-between="10"
      :loop="true"
      :navigation="true"
      :pagination="pagination"
      :autoplay="{ delay: 4500, disableOnInteraction: false }">
      <SwiperSlide v-for="(item, index) in slides" :key="index">
        <a :title="item.title" :href="item.fullPath" target="_blank">
          <div class="image-wrapper image-330">
            <img class="image lazy" :src="item.imageUrl" :alt="item.shortText" />
          </div>
        </a>
      </SwiperSlide>
    </Swiper>
  </div>
</template>
