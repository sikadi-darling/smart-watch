<template>
  <header class="main-header">
    <RouterLink to="/" class="logo">
      <img src="../assets/start-icon.png" alt="SW11 Logo" class="logo-icon" />
      <span>SW11</span>
    </RouterLink>
    
    <nav class="main-nav">
      <!-- 使用 RouterLink 来进行页面跳转 -->
      <RouterLink to="/">Main View</RouterLink>
      <RouterLink to="/about">About Us</RouterLink> <!-- 新增的链接 -->
      <RouterLink to="/product">Product Page</RouterLink>
      <RouterLink to="/support">Support</RouterLink>
    </nav>

    <RouterLink to="/#order" class="cta-button-header">Order Now</RouterLink>
  </header>
</template>

<script setup>
import { RouterLink } from 'vue-router';
</script>

<style scoped>
/* 这里是之前在HomeView.vue中的所有header相关样式 */
.main-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 5%;
  z-index: 100;
  background: var(--header-bg-color);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.logo {
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--primary-text-color); /* 确保文字颜色被应用 */
  text-shadow: 0 0 8px rgba(0, 217, 255, 0.3);
  display: flex;
  align-items: center;
  gap: 10px;
  text-decoration: none; /* 移除RouterLink的下划线 */
}

.logo-icon {
  height: 2.0rem; /* 使用您调整后的大小 */
  width: auto;
}

.main-nav a {
  color: var(--secondary-text-color);
  text-decoration: none;
  margin: 0 20px;
  font-size: 1rem;
  font-weight: 400;
  transition: color 0.3s ease, text-shadow 0.3s ease;
}

.main-nav a:hover,
.main-nav a.router-link-exact-active { /* 为当前活动链接添加高亮 */
  color: var(--primary-text-color);
  text-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
}

.cta-button-header {
  background-color: transparent;
  border: 1px solid var(--accent-color);
  color: var(--accent-color);
  padding: 10px 20px;
  border-radius: 50px;
  text-decoration: none;
  font-weight: 500;
  transition: all 0.3s ease;
  box-shadow: 0 0 15px rgba(0, 217, 255, 0.3);
}

.cta-button-header:hover {
  background-color: var(--accent-color);
  color: var(--bg-color);
  box-shadow: 0 0 25px rgba(0, 217, 255, 0.6);
}
</style>