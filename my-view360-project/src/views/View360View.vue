<template>
  <div class="view360-container">
    <div ref="viewer" class="viewer"></div>
    <div v-if="error" class="error-message">
      {{ error }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { PanoViewer } from '@egjs/view360'

const viewer = ref<HTMLElement | null>(null)
const error = ref<string | null>(null)

onMounted(() => {
  try {
    console.log('Viewer 마운트됨', viewer.value)
    
    if (viewer.value) {
      console.log('@egjs/view360 라이브러리 로드됨', PanoViewer)
      
      // PanoViewer 사용
      const view360 = new PanoViewer(viewer.value, {
        image: '/sample_360.jpg',
        useZoom: true
      })
      
      console.log('PanoViewer 인스턴스 생성됨', view360)
      
      // 이미지 로드 확인
      const img = new Image()
      img.onload = () => console.log('이미지 로드 성공')
      img.onerror = (e) => {
        console.error('이미지 로드 실패', e)
        error.value = '이미지 로드에 실패했습니다. 파일 경로를 확인해주세요.'
      }
      img.src = '/sample_360.jpg'
    }
  } catch (e) {
    console.error('에러 발생:', e)
    error.value = `에러가 발생했습니다: ${e instanceof Error ? e.message : String(e)}`
  }
})
</script>

<style scoped>
.view360-container {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.viewer {
  width: 100%;
  height: 100%;
}

.error-message {
  position: absolute;
  top: 20px;
  left: 20px;
  background-color: rgba(255, 0, 0, 0.7);
  color: white;
  padding: 10px;
  border-radius: 5px;
  max-width: 80%;
}
</style> 