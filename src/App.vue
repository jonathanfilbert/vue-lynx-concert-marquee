<script setup lang="ts">
import { ref, computed } from 'vue-lynx'

import './App.css'

type Theme = {
  name: string
  background: string
  text: string
  gradient?: string
}

const themes: Theme[] = [
  {
    name: 'Concert',
    background: '#000000',
    text: '#ff0000',
  },
  {
    name: 'Neon',
    background: '#0a0a0a',
    text: '#00ffcc',
    gradient: 'linear-gradient(135deg, #0a0a0a 0%, #1a1a2e 100%)',
  },
  {
    name: 'Sunset',
    background: '#1a0a1a',
    text: '#ff6b35',
    gradient: 'linear-gradient(135deg, #1a0a1a 0%, #2d2d44 100%)',
  },
]

const currentPage = ref<'entry' | 'display'>('entry')
const displayText = ref('')
const inputText = ref('')
const selectedThemeIndex = ref(0)

const currentTheme = computed(() => themes[selectedThemeIndex.value])

const containerStyle = computed(() => ({
  background: currentTheme.value.gradient || currentTheme.value.background,
}))

const textStyle = computed(() => ({
  color: currentTheme.value.text,
}))

function goToDisplay() {
  if (inputText.value.trim()) {
    displayText.value = inputText.value
    currentPage.value = 'display'
  }
}

function goToEntry() {
  currentPage.value = 'entry'
}

function selectTheme(index: number) {
  selectedThemeIndex.value = index
}
</script>

<template>
  <view class="app-container" :style="containerStyle">
    <!-- Entry Screen -->
    <view v-if="currentPage === 'entry'" class="entry-screen">
      <text class="title" :style="textStyle">Concert Marquee</text>
      <view class="input-container">
        <text class="label" :style="textStyle">Enter text to display:</text>
        <input :value="inputText" @input="(e) => inputText = e.detail.value" class="text-input" placeholder="Type here..." />
      </view>
      <view class="theme-selector">
        <view v-for="(theme, index) in themes" :key="theme.name" class="theme-circle" :class="{ 'theme-circle--selected': index === selectedThemeIndex }" @tap="selectTheme(index)" :style="{ background: theme.background }">
          <text class="theme-dot" :style="{ backgroundColor: theme.text }" />
        </view>
      </view>
      <view @tap="goToDisplay" class="display-button">
        <text class="button-text">Display</text>
      </view>
    </view>

    <!-- Display Screen -->
    <view v-if="currentPage === 'display'" class="display-screen" @tap="goToEntry">
      <view class="marquee-container">
        <text class="marquee-text" :style="textStyle">{{ displayText }}</text>
      </view>
    </view>
  </view>
</template>
