<template>
  <el-dialog
    title="视频播放"
    v-model="videoDialogVisible"
    width="800px"
    append-to-body
    destroy-on-close
    :close-on-click-modal="false"
  >
    <video width="100%" height="500px" controls :src="videoPath" style="object-fit: fill;">
      <track v-if="subtitlePath" kind="subtitles" :src="subtitlePath" srclang="zh" label="中文" default />
      您的浏览器不支持 HTML5 视频标签。
    </video>
  </el-dialog>
</template>

<script setup name="videoDialog">
import { ref, defineExpose } from 'vue';

const videoDialogVisible = ref(false);
const videoPath = ref('');
const subtitlePath = ref(''); // 新增字幕路径

const open = (videoUrl, subtitleUrl) => {
  videoPath.value = '';
  subtitlePath.value = '';
  videoDialogVisible.value = false;

  // Allow DOM update
  setTimeout(() => {
    videoPath.value = videoUrl;
    subtitlePath.value = subtitleUrl || '';
    videoDialogVisible.value = true;
  }, 50);
};


defineExpose({ open });
</script>

<style scoped lang="scss"></style>
