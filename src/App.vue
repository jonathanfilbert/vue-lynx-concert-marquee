<script setup lang="ts">
import { ref } from 'vue-lynx'

import './App.css'

const currentPage = ref<'entry' | 'display'>('entry')
const displayText = ref('')
const inputText = ref('')

function goToDisplay() {
  if (inputText.value.trim()) {
    displayText.value = inputText.value
    currentPage.value = 'display'
  }
}

function goToEntry() {
  currentPage.value = 'entry'
}
</script>

<template>
  <view class="app-container">
    <!-- Entry Screen -->
    <view v-if="currentPage === 'entry'" class="entry-screen">
      <text class="title">Concert Marquee</text>
      <view class="input-container">
        <text class="label">Enter text to display:</text>
        <input :value="inputText" @input="(e) => inputText = e.detail.value" class="text-input" placeholder="Type here..." />
      </view>
      <view @tap="goToDisplay" class="display-button">
        <text class="button-text">Display</text>
      </view>
    </view>

    <!-- Display Screen -->
    <view v-if="currentPage === 'display'" class="display-screen" @tap="goToEntry">
      <view class="marquee-container">
        <text class="marquee-text">{{ displayText }}</text>
      </view>
    </view>
  </view>
</template>
