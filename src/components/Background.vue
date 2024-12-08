<script setup>
import { ref, onMounted } from 'vue'

const backgroundImage = ref('')
const backgroundOpacity = ref(0.1)
const settingsVisible = ref(false)

const handleSetBackground = (url) => {
  backgroundImage.value = url
  window.localStorage.setItem('background_image', url)
}

const handleSetOpacity = (opacity) => {
  backgroundOpacity.value = opacity
  window.localStorage.setItem('background_opacity', opacity)
}

const handleShowSettings = () => {
  settingsVisible.value = true
}

const handleClose = () => {
  settingsVisible.value = false
}

const handleConfirm = (url, opacity) => {
  handleSetBackground(url)
  handleSetOpacity(opacity)
  settingsVisible.value = false
}

const handleFileChange = (e) => {
  const file = e.target.files[0]
  if (file) {
    const reader = new FileReader()
    reader.onload = (e) => {
      handleSetBackground(e.target.result)
    }
    reader.readAsDataURL(file)
  }
}

onMounted(() => {
  backgroundImage.value = window.localStorage.getItem('background_image') || ''
  backgroundOpacity.value = parseFloat(window.localStorage.getItem('background_opacity')) || 0.1
})
</script>

<template>
  <div class="background-wrapper">
    <!-- 背景图片容器 -->
    <div class="background-container" v-if="backgroundImage">
      <img :src="backgroundImage" :style="{opacity: backgroundOpacity}" />
    </div>

    <!-- 设置按钮 -->
    <div class="background-settings">
      <a-button class="settings-btn" :shape="'round'" @click="handleShowSettings">
        <template #icon>
          <icon-image />
        </template>
      </a-button>
    </div>

    <!-- 设置对话框 -->
    <a-modal
      v-model:visible="settingsVisible"
      :footer="false"
      :hide-title="true"
      width="360px"
    >
      <div class="akile-modal-title">
        <span>背景设置</span>
        <a-button @click="handleClose">
          <template #icon>
            <icon-close/>
          </template>
        </a-button>
      </div>
      <div class="akile-modal-content">
        <a-input
          v-model="backgroundImage"
          placeholder="填入你的壁纸地址或者URL"
          style="margin-bottom: 10px;"
        />
        <input
          type="file"
          accept="image/*"
          @change="handleFileChange"
          style="margin-bottom: 10px;"
        />
        <a-slider
          v-model="backgroundOpacity"
          :min="0"
          :max="1"
          :step="0.1"
          style="margin-bottom: 10px;"
        />
      </div>
      <div class="akile-modal-action">
        <a-button type="primary" :long="true" @click="handleConfirm(backgroundImage, backgroundOpacity)">
          确认设置
        </a-button>
      </div>
    </a-modal>
  </div>
</template>

<style lang="scss" scoped>
.background-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.background-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: opacity 0.3s ease;
  }
}

.background-settings {
  position: fixed;
  right: 20px;
  bottom: 20px;
  z-index: 1000;
  pointer-events: auto;
  
  .settings-btn {
    border: 1px solid #eeeeee;
    background-color: #ffffff;
    color: #333333;
    
    &:hover {
      background-color: #f5f5f5;
    }
  }
}

:global(body[arco-theme='dark']) {
  .background-settings {
    .settings-btn {
      border: 1px solid #333333;
      background-color: #000000;
      color: #ffffff;
      
      &:hover {
        background-color: #1a1a1a;
      }
    }
  }
}
</style> 