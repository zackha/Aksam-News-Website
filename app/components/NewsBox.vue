<script setup>
defineProps({ newsList: { type: Array, required: true } });
</script>
<template>
  <div v-for="(news, index) in newsList" :key="index" class="col-3">
    <div class="item relative">
      <a class="full-link" :href="news.fullPath" :title="news.title" target="_blank"></a>

      <div class="image-wrapper image-150">
        <img class="image" :src="news.imageUrl" :alt="news.shortText" />
      </div>
      <div class="text">
        <div class="category category7"></div>
        <h3 class="font-weight-7 font-size-16">{{ news.title }}</h3>
      </div>
    </div>
  </div>
</template>
