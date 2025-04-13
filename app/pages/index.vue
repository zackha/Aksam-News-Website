<script setup>
const { data: anasayfaData } = await useFetch('/api/anasayfa');

useSeoMeta({
  title: 'AKŞAM - Haberler - Son Dakika Haberleri',
  description: "Gündemden son dakika haberleri, tüm dünyadan gelişmeler, öne çıkan haber başlıkları Akşam'da.",
  keywords:
    'haber, haberler, son dakika haberleri, son dakika istanbul, son dakika dünya, son dakika ankara, son dakika, en son haber, flaş haber, son gelişme, güncel haber, internet haber, türkiye haberleri, gazete manşetleri',
  ogTitle: 'AKŞAM Haberler - Son Dakika Haberleri, Güncel İnternet Haberleri',
  ogDescription: "Gündemden son dakika haberleri, tüm dünyadan gelişmeler, öne çıkan haber başlıkları Akşam'da.",
  ogType: 'website',
  ogUrl: 'https://www.aksam.com.tr/',
  ogSiteName: 'Akşam',
  ogImage: 'https://www.aksam.com.tr/images/aksam-face.png',
  ogImageType: 'image/png',
  ogImageWidth: '200',
  ogImageHeight: '200',
  ogLocale: 'tr_TR',
  twitterCard: 'summary_large_image',
  twitterSite: '@aksam',
  twitterTitle: 'Akşam Anasayfa',
  twitterDescription: "Gündemden son dakika haberleri, tüm dünyadan gelişmeler, öne çıkan haber başlıkları Akşam'da.",
  twitterCreator: '@aksam',
  twitterImage: 'https://www.aksam.com.tr/images/aksam-logo.svg',
  facebookDomainVerification: '5lxhuqjthjdnxj8s8aqfue4tq7qlwp',
  author: 'aksam.com.tr',
  viewport: 'width=device-width, initial-scale=1',
});

useHead({
  htmlAttrs: {
    lang: 'tr',
  },
  meta: [
    { charset: 'utf-8' },
    { 'http-equiv': 'X-UA-Compatible', content: 'IE=edge' },
    { name: 'apple-itunes-app', content: 'app-id=982894881' },
    { name: 'google-play-app', content: 'app-id=com.aksam.android' },
    { name: 'bitly-verification', content: '990a736d5c15' },
  ],
  link: [
    { rel: 'canonical', href: 'https://www.aksam.com.tr/' },
    { rel: 'alternate', media: 'only screen and (max-width: 640px)', href: 'https://m.aksam.com.tr/' },
    { rel: 'apple-touch-icon', href: 'https://www.aksam.com.tr/images/apple-touch-icon.png' },
    { rel: 'icon', type: 'image/png', href: 'https://www.aksam.com.tr/assets-aksam/img/favicon.png' },
  ],
  script: [
    {
      type: 'application/ld+json',
      children: JSON.stringify({
        '@context': 'https://schema.org',
        '@type': 'Organization',
        name: 'Akşam',
        brand: 'Akşam',
        alternateName: 'aksam.com.tr',
        memberOf: {
          '@type': 'Organization',
          name: 'TürkMedya',
        },
        description: "Gündemden son dakika haberleri, tüm dünyadan gelişmeler, öne çıkan haber başlıkları Akşam'da.",
        url: 'https://www.aksam.com.tr/',
        slogan: "Türkiye'nin Gazetesi Akşam'ı takip edin hayattan kopmayın!",
        email: 'webmaster@aksam.com.tr',
        foundingDate: '1918-09-20',
        logo: 'https://www.aksam.com.tr/images/aksam-logo.svg',
        sameAs: ['https://www.facebook.com/Aksam/', 'https://twitter.com/aksam', 'https://www.youtube.com/user/aksamgazetesi', 'https://www.instagram.com/aksam/'],
        contactPoint: [
          {
            '@type': 'ContactPoint',
            telephone: '+902124732000',
            contactType: 'customer service',
            contactOption: 'TollFree',
            areaServed: 'TR',
          },
        ],
      }),
    },
  ],
});

const swipeItems = computed(() => anasayfaData.value?.data.find(section => section.sectionType === 'SWIPE')?.itemList || []);

const newsItems = computed(() => anasayfaData.value?.data.find(section => section.sectionType === 'NEWS')?.itemList || []);

const lastNewsOne = computed(() => swipeItems.value.slice(0, 8));
const lastNewsTwo = computed(() => swipeItems.value.slice(8, 13));

const newsBoxItems = computed(() => newsItems.value.slice(0, 4));
const sliderItems = computed(() =>
  newsItems.value.slice(4).map(item => {
    const timeParts = item.publishDate?.split(' ')[1]?.split(':') || [];
    const time = timeParts.length >= 2 ? `${timeParts[0]}:${timeParts[1]}` : '';
    return {
      title: item.title,
      href: item.fullPath || '#',
      time,
    };
  })
);
</script>

<template>
  <div class="shell">
    <Header />
    <div class="container">
      <div class="margin-bottom-md">
        <div class="row">
          <LastNewsOne :slides="lastNewsOne" />
          <LastNewsTwo :slides="lastNewsTwo" />
        </div>
      </div>
      <div class="box-news-1 margin-bottom-md">
        <div class="row">
          <NewsBox :newsList="newsBoxItems" />
        </div>
      </div>
      <Slider :newsItems="sliderItems" />
    </div>
  </div>
</template>
