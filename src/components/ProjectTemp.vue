<template>
    <div class="items-center justify-center flex-auto h-7">
        <n-card :title="project.name" size="small" class="max-w-xs ">
            <template #cover>
                <img :src="project.cover">
            </template>
            <template #header-extra>
            不错
            </template>
            卡片内容
            <template #action>
                <n-button strong secondary round type="primary" @click="visit">
                    访问
                </n-button>
            </template>
        </n-card>
    </div>
</template>

<script setup lang="ts">
import { reactive } from 'vue';

const project = reactive({
    name: 'Blog',
    description: 'This is a project template',
    url: 'https://blog.bangwu.top',
    cover: 'https://07akioni.oss-cn-beijing.aliyuncs.com/07akioni.jpeg'
});

const visit = () => {
    window.open(project.url);
}
</script>

<style scoped>

</style>