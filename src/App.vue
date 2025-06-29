<script setup>
import { RouterView } from 'vue-router'
import MainHeader from './components/MainHeader.vue' // 引入共享导航栏
</script>

<template>
  <MainHeader />
  <main>
    <RouterView />
  </main>
</template>

<style>
/* 全局样式保持不变 */
:root {
  --bg-color: #040713; 
  --accent-color: #00d9ff; 
  --primary-text-color: #ffffff;
  --secondary-text-color: #a0a0b0;
  --header-bg-color: rgba(5, 8, 24, 0.7);
}
* { margin: 0; padding: 0; box-sizing: border-box; }
body, html {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  overscroll-behavior: none;
  background: radial-gradient(ellipse at center, #10182f 0%, var(--bg-color) 70%);
  color: var(--primary-text-color);
}
</style>