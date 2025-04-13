<script setup>
defineProps({ newsItems: { type: Array, required: true } });
</script>
<template>
  <div class="last-news margin-bottom-md flex middle" id="lastnews">
    <div class="swiper-container width-full">
      <ul class="swiper-wrapper">
        <li v-for="(item, index) in newsItems" :key="index" class="swiper-slide">
          <a class="flex center" :href="item.href" target="_blank">
            <div class="time font-size-12 margin-right-sm">{{ item.time }}</div>
            <h3 class="title">{{ item.title }}</h3>
          </a>
        </li>
      </ul>
    </div>
    <div class="navigation flex middle mlm">
      <Icon name="heroicons:chevron-left-solid" class="icon cursor-pointer icon-left-arrow-line font-size-18" />
      <Icon name="heroicons:chevron-right-solid" class="icon cursor-pointer icon-right-arrow-line font-size-18 margin-right-sm" />
      <a class="f14" href="#">Tümü</a>
    </div>
  </div>
</template>
