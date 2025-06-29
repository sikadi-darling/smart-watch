<template>
  <div class="about-page">
    <div class="content-wrapper">
      <!-- Company Profile Section -->
      <section class="profile-section">
        <h2>Company Profile</h2>
        <p>
          666 Company is a high-tech enterprise specializing in the R & D and production of smart wearable devices. It is committed to providing users with innovative and convenient smart life solutions. Since its establishment, with the mission of “Technology Changing Life”, we have successfully launched a number of popular smart watch products, covering core functions such as health monitoring, sports tracking, and smart notifications. Relying on advanced technology R & D capabilities and a strict quality management system, 666 Company has become one of the leading brands in the smart wearable industry. In the future, we will continue to deepen artificial intelligence and Internet of Things technologies, create smarter and more human-centered products, and promote the development of the global smart wearable ecosystem.
        </p>
      </section>

      <!-- Personnel Introduction Section -->
       <section class="personnel-section">
        <h2>Our Team</h2>
        <div class="personnel-grid">
          <!-- [模板改动] 卡片内部增加了SVG图标 -->
          <!-- [模板改动] 在卡片内部增加了用于描绘边框的 SVG -->
          <div v-for="member in team" :key="member.name" class="personnel-card">
            <!-- 动态边框 SVG -->
            <svg class="card-border" width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
              <rect width="100%" height="100%" rx="10" ry="10" />
            </svg>
            
            <!-- 原有内容 -->
            <div class="icon-container">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="personnel-icon" v-html="member.icon"></svg>
            </div>
            <div class="text-content">
              <h3>{{ member.name }}</h3>
              <p class="role">{{ member.role }}</p>
              <p class="description">{{ member.description }}</p>
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
// 1. 引入 ScrollTrigger 插件
import { ScrollTrigger } from 'gsap/ScrollTrigger';

// 2. 注册插件，这是必须的步骤！
gsap.registerPlugin(ScrollTrigger);

// [数据改动] 为每个成员添加了'icon'字段，包含SVG的<path>数据
const team = ref([
  { name: 'Su Yongcheng', role: 'General Manager', icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0zM4.501 20.118a7.5 7.5 0 0114.998 0A17.933 17.933 0 0112 21.75c-2.676 0-5.216-.584-7.499-1.632z" />', description: 'Responsible for the overall strategic planning and operation management of the company.' },
  { name: 'Li Sihan', role: 'Technical Director', icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M8.25 3v1.5M4.5 8.25H3m18 0h-1.5M4.5 12H3m18 0h-1.5m-15 3.75H3m18 0h-1.5M8.25 19.5V21M12 3v1.5m0 15V21m3.75-18v1.5m0 15V21m-9-1.5h10.5a2.25 2.25 0 002.25-2.25V8.25a2.25 2.25 0 00-2.25-2.25H8.25A2.25 2.25 0 006 8.25v10.5A2.25 2.25 0 008.25 19.5z" />', description: 'Leads the R & D team for smart watch software and hardware.' },
  { name: 'Mo Zuchao', role: 'Product Manager', icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M12 18v-5.25m0 0a6.01 6.01 0 001.5-.189m-1.5.189a6.01 6.01 0 01-1.5-.189m3.75 7.478a12.06 12.06 0 01-4.5 0m3.75 2.354a12.06 12.06 0 01-4.5 0m4.5 2.354a12.06 12.06 0 01-4.5 0M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />', description: 'Responsible for the product design, function planning, and user experience improvement.' },
  { name: 'Fan Lihong', role: 'Production Director', icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M10.5 6h9.75M10.5 6a1.5 1.5 0 11-3 0m3 0a1.5 1.5 0 10-3 0M3.75 6H7.5m3 12h9.75m-9.75 0a1.5 1.5 0 01-3 0m3 0a1.5 1.5 0 00-3 0m-3.75 0H7.5m9-6h3.75m-3.75 0a1.5 1.5 0 01-3 0m3 0a1.5 1.5 0 00-3 0m-9.75 0h9.75" />', description: 'Manages the production process and optimizes the supply chain and quality control.' },
  { name: 'Xu Haijian', role: 'Marketing Director', icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M10.5 1.5H8.25A2.25 2.25 0 006 3.75v16.5a2.25 2.25 0 002.25 2.25h7.5A2.25 2.25 0 0018 20.25V3.75a2.25 2.25 0 00-2.25-2.25H13.5m-3 0V3h3V1.5m-3 0h3m-3 18.75h3" />', description: 'Formulates brand promotion strategies and coordinates marketing activities.' },
  { name: 'Zhu Haomin', role: 'Sales Manager', icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M2.25 18.75a60.07 60.07 0 0115.797 2.101c.727.198 1.453-.342 1.453-1.096V18.75M3.75 4.5v.75A.75.75 0 013 6h-.75m0 0v-.375c0-.621.504-1.125 1.125-1.125H20.25M2.25 6v9m18-10.5v.75c0 .414.336.75.75.75h.75m-1.5-1.5h.375c.621 0 1.125.504 1.125 1.125v9.75c0 .621-.504 1.125-1.125 1.125h-.375m1.5-1.5H21a.75.75 0 00-.75.75v.75m0 0H3.75m0 0h-.375a1.125 1.125 0 01-1.125-1.125V15m1.5 1.5v-.75A.75.75 0 003 15h-.75M15 10.5a3 3 0 11-6 0 3 3 0 016 0z" />', description: 'Responsible for domestic and foreign market sales and customer relationship maintenance.' },
  { name: 'Liang Jialin', role: 'Software Engineer', icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M17.25 6.75L22.5 12l-5.25 5.25m-10.5 0L1.5 12l5.25-5.25m7.5-3l-4.5 16.5" />', description: 'Participates in the development of the smart watch operating system and algorithm optimization.' },
  // --- 这一行被修改了 ---
  { name: 'Li Wanyang', role: 'Hardware Engineer', icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6A2.25 2.25 0 016 3.75h2.25A2.25 2.25 0 0110.5 6v2.25a2.25 2.25 0 01-2.25 2.25H6a2.25 2.25 0 01-2.25-2.25V6zM3.75 15.75A2.25 2.25 0 016 13.5h2.25a2.25 2.25 0 012.25 2.25V18a2.25 2.25 0 01-2.25 2.25H6A2.25 2.25 0 013.75 18v-2.25zM13.5 6a2.25 2.25 0 012.25-2.25H18A2.25 2.25 0 0120.25 6v2.25A2.25 2.25 0 0118 10.5h-2.25a2.25 2.25 0 01-2.25-2.25V6zM13.5 15.75a2.25 2.25 0 012.25-2.25H18a2.25 2.25 0 012.25 2.25V18A2.25 2.25 0 0118 20.25h-2.25A2.25 2.25 0 0113.5 18v-2.25z" />', description: 'Leads the design and testing of hardware modules such as sensors and chips.' 
}
]);
onMounted(() => {
  // 3. 创建动画
  // 动画 A: 公司简介部分 (标题和段落)
  // 当 .profile-section 滚动到视野内时触发
  gsap.from(".profile-section h2", {
    scrollTrigger: ".profile-section", // 触发器
    duration: 0.8,
    y: 50,
    opacity: 0,
    ease: "power3.out",
  });
  gsap.from(".profile-section p", {
    scrollTrigger: ".profile-section",
    duration: 1.2,
    y: 50,
    opacity: 0,
    ease: "power3.out",
    delay: 0.2, // 比标题稍晚出现
  });

  // 动画 B: 团队介绍部分的标题
  gsap.from(".personnel-section h2", {
    scrollTrigger: ".personnel-section",
    duration: 0.8,
    y: 50,
    opacity: 0,
    ease: "power3.out",
  });

  // 动画 C: 团队成员卡片网格 - 这是最精彩的部分！
  // 使用 stagger 交错效果，让卡片逐一出现

  gsap.from(".personnel-card", {
    scrollTrigger: {
      trigger: ".personnel-grid",
      start: "top 85%",
    },
    duration: 0.6,
    y: 40,
    opacity: 0,
    ease: "power3.out",
    stagger: 0.1,
    // [新增] onComplete 回调，在入场动画完成后再初始化悬停效果
    onComplete: initCardHoverAnimations,
  });
  
  // --- 新增：初始化卡片悬停动画的函数 ---
  function initCardHoverAnimations() {
    const cards = document.querySelectorAll('.personnel-card');

    cards.forEach(card => {
      const rect = card.querySelector('.card-border rect');
      const iconContainer = card.querySelector('.icon-container');

      // 1. 计算 SVG 矩形的周长，这是“绘制”动画的关键
      const width = rect.getAttribute('width');
      const height = rect.getAttribute('height');
      // 注意：由于width/height是"100%"，我们需要获取元素的实际尺寸
      const perimeter = (card.offsetWidth + card.offsetHeight) * 2;
      
      // 2. 设置 SVG 描边的初始状态
      // stroke-dasharray: 创建虚线，长度为周长
      // stroke-dashoffset: 将虚线起始点偏移一个周长，使其完全隐藏
      gsap.set(rect, {
        strokeDasharray: perimeter,
        strokeDashoffset: perimeter,
      });

      // 3. 创建一个可复用的 GSAP 时间线 (timeline)，初始状态为暂停
      const tl = gsap.timeline({ paused: true, defaults: { duration: 0.4, ease: 'power2.out' } });

      // 4. 定义时间线上的动画序列
      tl.to(card, { scale: 1.05, boxShadow: '0 15px 40px rgba(0, 0, 0, 0.4)' }) // 卡片放大并增加更深的阴影
        .to(iconContainer, { scale: 1.1, y: -5 }, '<') // 图标放大并轻微上移 ( '<' 表示与上一动画同时开始)
        .to(rect, { strokeDashoffset: 0 }, '<'); // 描边动画：将偏移量归零，"画"出边框

      // 5. 绑定鼠标事件来控制时间线的播放和反向播放
      card.addEventListener('mouseenter', () => tl.play());
      card.addEventListener('mouseleave', () => tl.reverse());
    });
  }

});
</script>

<style scoped>
.about-page {
  padding: 120px 5% 60px; /* 顶部120px是为了给固定的导航栏留出空间 */
  min-height: 100vh;
  box-sizing: border-box;
}

.content-wrapper {
  max-width: 1200px;
  margin: 0 auto;
}

h2 {
  font-size: 2.5rem;
  color: var(--accent-color);
  text-shadow: 0 0 10px rgba(0, 217, 255, 0.5);
  margin-bottom: 30px;
  padding-bottom: 10px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
}

.profile-section p {
  font-size: 1.1rem;
  line-height: 1.8;
  color: var(--secondary-text-color);
  max-width: 900px;
  margin-bottom: 60px;
}

.personnel-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
}

.personnel-card {
  background-color: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  padding: 25px;
  /* [改动] 移除 transition，因为 GSAP 会处理 */
  /* transition: transform 0.3s ease, box-shadow 0.3s ease, border-color 0.3s ease; */
  display: flex;
  gap: 20px;
  align-items: flex-start;
  /* [新增] 关键！为内部绝对定位的 SVG 提供定位上下文 */
  position: relative;
  /* [新增] 防止内部元素在放大时溢出卡片圆角 */
  overflow: hidden;
}

/* [改动] 移除旧的 hover 样式 */
/*
.personnel-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  border-color: var(--accent-color);
}
*/

/* [新增] 动态边框 SVG 的样式 */
.card-border {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none; /* 确保 SVG 不会捕获鼠标事件 */
}

.card-border rect {
  fill: none;
  stroke: var(--accent-color);
  stroke-width: 2px; /* 边框宽度 */
  /* 让边框看起来更亮眼 */
  filter: drop-shadow(0 0 5px var(--accent-color));
}


.icon-container {
  flex-shrink: 0;
  background-color: rgba(0, 217, 255, 0.1);
  border-radius: 50%;
  padding: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  /* [新增] 将 z-index 提高，确保它在 SVG 边框之上 */
  z-index: 1;
}

.personnel-icon {
  width: 32px;
  height: 32px;
  color: var(--accent-color);
}

.text-content {
  display: flex;
  flex-direction: column;
  /* [新增] 同样提高 z-index */
  z-index: 1;
}


.personnel-card h3 {
  font-size: 1.5rem;
  color: var(--primary-text-color);
  margin-bottom: 5px;
}

.personnel-card .role {
  font-size: 1rem;
  font-weight: 500;
  color: var(--accent-color);
  margin-bottom: 15px;
}

.personnel-card .description {
  font-size: 0.95rem;
  color: var(--secondary-text-color);
  line-height: 1.6;
}
</style>