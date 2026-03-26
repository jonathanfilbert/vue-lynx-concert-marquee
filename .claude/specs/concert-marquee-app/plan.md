# Concert Marquee App - Implementation Plan

## Overview
Create a simple Vue App for concerts that displays a marquee of large red text horizontally scrolling over a black background. The app will have two screens/states.

## Requirements
1. **Word Entry Screen**: Input field for text + "Display" button
2. **Display Screen**: Shows the inputted text in very large size, scrolling horizontally at a predefined speed
3. **Visual Style**: Black background, red text, large font size suitable for concert displays

## Technical Approach

### VueLynx Compatibility Notes
**IMPORTANT**: Native `<input>` does NOT support `v-model`. Must use `:value` with `@input` event:
```vue
<input :value="inputText" @input="(e) => inputText = e.detail.value" />
```

### State Management
- Use Vue 3 Composition API with `ref()` for reactive state
- Two states:
  - `currentPage`: 'entry' | 'display' - controls which screen is shown
  - `displayText`: string - stores the text to display on the marquee
  - `inputText`: string - stores the current input field value

### Animation Strategy
- Use CSS animations for smooth horizontal scrolling
- CSS `@keyframes` for continuous scrolling effect
- Transform-based animation for better performance (GPU acceleration)

### File Modifications

#### 1. Modify `src/App.vue`
- Replace existing demo content with new concert marquee app
- Implement two conditional views based on `currentPage` state
- Use `<view>` and `<text>` components from vue-lynx

**Structure:**
```
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
```

#### 2. Modify `src/App.css`
- Completely replace existing styles with concert marquee styles
- Implement black background and red text theme
- Add marquee scrolling animation

**Key Styles:**
```css
:root {
  background-color: #000;
}

.app-container {
  min-height: 100vh;
  background-color: #000;
  display: flex;
  flex-direction: column;
}

/* Entry Screen Styles */
.entry-screen {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 40rpx;
  min-height: 100vh;
}

.title {
  color: #ff0000;
  font-size: 48rpx;
  font-weight: bold;
  margin-bottom: 60rpx;
}

.input-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 80%;
  margin-bottom: 60rpx;
}

.label {
  color: #fff;
  font-size: 32rpx;
  margin-bottom: 20rpx;
}

.text-input {
  width: 100%;
  height: 100rpx;
  background-color: #1a1a1a;
  border: 2rpx solid #ff0000;
  color: #fff;
  font-size: 36rpx;
  padding: 20rpx;
}

.display-button {
  background-color: #ff0000;
  padding: 30rpx 80rpx;
  border-radius: 10rpx;
}

.button-text {
  color: #fff;
  font-size: 40rpx;
  font-weight: bold;
}

/* Display Screen Styles */
.display-screen {
  min-height: 100vh;
  background-color: #000;
  display: flex;
  align-items: center;
  overflow: hidden;
}

.marquee-container {
  width: 100%;
  overflow: hidden;
  white-space: nowrap;
}

.marquee-text {
  color: #ff0000;
  font-size: 120rpx;
  font-weight: bold;
  display: inline-block;
  animation: marquee 10s linear infinite;
}

@keyframes marquee {
  0% {
    transform: translateX(100%);
  }
  100% {
    transform: translateX(-100%);
  }
}
```

### Implementation Steps

1. **Clean up existing code**
   - Remove unused imports (arrow, logos, useFlappy)
   - Remove unused files (assets that won't be used)

2. **Implement App.vue**
   - Add state management refs
   - Create entry screen with input and button
   - Create display screen with marquee text
   - Add navigation logic between screens

3. **Implement App.css**
   - Set up black background
   - Style entry screen components
   - Style display screen with marquee animation
   - Ensure red text color throughout

4. **Testing and Build Verification**
   - Use bun for all package management and building
   - Run `bun run build` to verify the build succeeds
   - Test text input with various lengths
   - Verify marquee animation is smooth
   - Test navigation between screens
   - Verify tap areas are responsive
   - Test on actual Lynx device if available

### Build Commands
- `bun run dev` - Start development server
- `bun run build` - Build for production (must verify this succeeds)
- `bun run preview` - Preview production build

## Notes
- **VueLynx Input**: Native `<input>` does NOT support `v-model` - must use `:value` and `@input="(e) => inputText = e.detail.value"`
- The marquee speed is set to 10s per cycle in CSS; this can be adjusted in the `@keyframes` animation duration
- The font size (120rpx) can be increased for larger displays
- The app uses simple tap navigation - tapping the display screen returns to entry
- No validation beyond checking for non-empty input
- The animation loops infinitely while on the display screen
