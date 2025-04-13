<script setup>
defineProps({ slides: { type: Array, required: true } });
const activeSlide = ref(0);
</script>

<template>
  <div class="col-8">
    <div class="slider-s-1" id="sliders1">
      <div class="swiper-container">
        <div class="swiper-wrapper">
          <div v-for="(slide, index) in slides" :key="index" class="swiper-slide">
            <a :href="slide.fullPath" :title="slide.title" target="_blank">
              <div class="image-wrapper image-330">
                <img class="image" :src="slide.imageUrl" :alt="slide.shortText" />
              </div>
            </a>
          </div>
        </div>
      </div>
      <ul class="s-pagination">
        <li v-for="(slide, index) in slides" :key="'pagination-' + index" :class="{ active: index === activeSlide }">
          <a :href="slide.fullPath" :title="slide.title" target="_blank">
            {{ index + 1 }}
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>
