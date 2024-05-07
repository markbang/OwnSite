<template>
    <div class="container p-4 mx-auto">
      <div class="px-8 pt-6 pb-8 mb-4 bg-white rounded shadow-md">
        <h1 class="mb-4 text-2xl font-bold">Telegram Channel</h1>
        <div v-if="loading" class="text-center">
          <p class="text-gray-600">Loading...</p>
        </div>
        <div v-else>
            <div v-for="item in items as any[]" :key="item.title" class="mb-4">
            <h2 class="mb-2 text-xl font-semibold">{{ renderTitle((item as any).title) }}</h2>
            <div v-html="renderHtml(replaceCdnUrl((item as any).description))" class="text-gray-700 border-2"></div>
            <hr>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted } from 'vue'
  import X2js from 'x2js'
  
  const rss_url = 'https://rsshub.bangwu.top/telegram/channel/markbangchannel'
  let x2js = new X2js()
  
  const loading = ref(true)
  const items = ref([])
  
  onMounted(async () => {
    try {
      const res = await fetch(rss_url)
      const data = await res.text()
      const json = x2js.xml2js(data)
      items.value = Array.isArray((json as any).rss.channel.item) ? (json as any).rss.channel.item : [(json as any).rss.channel.item]
      loading.value = false
    } catch (error) {
      console.error('Error fetching data:', error)
      loading.value = false
    }
  })
  
  const renderHtml = (html: string) => {
    return html.replace(/<img/g, '<img class="max-w-full mb-4"');
  }
  
  const renderTitle = (title: string) => {
    // Remove 'source' from title
    return title.replace(/\bsource\b/g, '').trim();
  }
  
  const replaceCdnUrl = (description: string) => {
    return description.replace(/cdn4\.cdn-telegram\.org/g, 'tg.313797.xyz');
  }
  </script>
  
  <style>
  /* You can add custom styles here */
  /* Material Design UI for title */
  .container h2 {
    font-size: 1.5rem;
    line-height: 2rem;
    color: rgba(0, 0, 0, 0.87);
    font-weight: 500;
  }
  /* Material Design UI for description */
  .container p {
    font-size: 1rem;
    line-height: 1.5rem;
    color: rgba(0, 0, 0, 0.6);
  }
  </style>
  