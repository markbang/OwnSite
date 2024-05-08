<template>
  <div class="container p-4 mx-auto">
    <div class="grid grid-cols-1 gap-4 md:grid-cols-3">
      <div v-for="item in items" :key="item.title" class="relative">
        <div class="overflow-hidden bg-white rounded-md shadow-md widget-card h-80">
          <div class="p-4">
            <h2 class="mb-2 text-xl font-semibold">{{ renderTitle(item.title) }}</h2>
            <div v-html="renderHtml(replaceCdnUrl(item.description))" class="text-gray-700"></div>
          </div>
          <div class="absolute bottom-0 left-0 right-0 p-4 bg-gray-100">
            <button @click="showDetails(item)" class="text-blue-500 hover:underline">查看详情</button>
          </div>
        </div>
      </div>
    </div>
    <div v-if="loading" class="mt-4 text-center">
      <p class="text-gray-600">加载中...</p>
    </div>
    <div v-if="showPopup" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
      <div class="max-w-md p-8 overflow-auto bg-white rounded-md shadow-md popup-content">
        <h2 class="mb-4 text-2xl font-bold">{{ selectedTitle }}</h2>
        <div v-html="renderHtml(replaceCdnUrl(selectedDescription))" class="text-gray-700"></div>
        <div class="mt-4 text-right">
          <button @click="closePopup" class="text-blue-500 hover:underline">关闭</button>
        </div>
      </div>
    </div>
  </div>
</template>




<script setup lang="ts">
import { ref, onMounted } from 'vue'
import X2js from 'x2js'

interface RSSItem {
  title: string;
  description: string;
  link: string;
}

const rss_url: string = 'https://rsshub.bangwu.top/telegram/channel/markbangchannel'
const x2js: any = new X2js()

const loading = ref<boolean>(true)
const items = ref<RSSItem[]>([])
const showPopup = ref<boolean>(false)
const selectedTitle = ref<string>('')
const selectedDescription = ref<string>('')

onMounted(async () => {
  try {
    const res: Response = await fetch(rss_url)
    const data: string = await res.text()
    const json: any = x2js.xml2js(data)
    items.value = Array.isArray(json.rss.channel.item) ? json.rss.channel.item : [json.rss.channel.item]
    loading.value = false
  } catch (error) {
    console.error('Error fetching data:', error)
    loading.value = false
  }
})

const renderHtml = (html: string): string => {
  return html.replace(/<img/g, '<img style="max-width: 100%; height: auto; object-fit: contain;"')
}

const renderTitle = (title: string): string => {
  return title.replace(/\bsource\b/g, '').trim()
}

const replaceCdnUrl = (description: string): string => {
  return description.replace(/cdn4\.cdn-telegram\.org/g, 'tg.313797.xyz')
}

const showDetails = (item: RSSItem) => {
  selectedTitle.value = item.title
  selectedDescription.value = item.description
  showPopup.value = true
}

const closePopup = () => {
  showPopup.value = false
}
</script>

<style>
.container {
  display: flex;
  justify-content: center;
}

/* Card styles */
.widget-card {
  height: 360px;
}

/* Popup styles */
.fixed {
  position: fixed;
}

.inset-0 {
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}

.flex {
  display: flex;
}

.justify-center {
  justify-content: center;
}

.items-center {
  align-items: center;
}

.bg-opacity-50 {
  background-color: rgba(0, 0, 0, 0.5);
}

.max-w-md {
  max-width: 32rem;
}

/* Popup content styles */
.popup-content {
  width: 90%;
  max-height: 90%;
  overflow-y: auto
}

/* Custom scrollbar styles */
.popup-content::-webkit-scrollbar {
  width: 8px;
}

.popup-content::-webkit-scrollbar-thumb {
  background-color: rgba(0, 0, 0, 0.3);
  border-radius: 4px;
}

.popup-content::-webkit-scrollbar-track {
  background-color: rgba(0, 0, 0, 0.1);
}
</style>
