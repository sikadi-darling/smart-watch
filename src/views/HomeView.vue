<template>
  <div class="product-page">
    <!-- Hero Section -->
    <main class="hero-section">
      <div class="hero-content">
        <div class="hero-text">
          <h1>SW11 Smart Watch</h1>
          <p>Intelligence Redefined. Power on Your Wrist.</p>
          <!-- [改动] 这里的 href 指向了新内容区的起始位置 -->
          <a href="#feature-sections" class="cta-button-main">Explore The Future</a>
        </div>
      </div>
      <div class="hero-image">
        <img src="../assets/sw11-watch.jpg" alt="SW11 Smart Watch" />
      </div>
    </main>

    <!-- [新增] 功能介绍区容器 -->

    <div id="feature-sections" class="feature-sections-container">

      <!-- Feature 1: AR Interaction -->
      <section class="feature-section ar-section">
        <div class="feature-text">
          <h2>Merge Your Worlds</h2>
          <h3>Augmented Reality on Your Wrist</h3>
          <p>
            Experience navigation, gaming, and learning like never before. 
            The SW11 projects interactive AR overlays into your environment. 
            Follow floating arrows to your destination, view 3D models of products, or play immersive games that blend the digital with the real.
          </p>
        </div>
        <div class="feature-image">
          <!-- [图片占位] 请替换为你自己的图片 -->
          <img src="../assets/ar-interaction.jpg" alt="Augmented Reality Interaction" />
        </div>
      </section>

      <!-- Feature 2: AI Translation -->
      <section class="feature-section layout-reverse translation-section">
        <div class="feature-text">
          <h2>Break Down Barriers</h2>
          <h3>Real-time AI Translation</h3>
          <p>
            Communicate effortlessly in over 50 languages. Our cutting-edge AI provides instant, two-way voice translation directly through the watch. 
            Whether you're traveling the world or in a multinational business meeting, the SW11 is your universal translator.
          </p>
        </div>
        <div class="feature-image">
           <!-- [图片占位] 请替换为你自己的图片 -->
          <img src="../assets/ai-translation.jpg" alt="AI Simultaneous Translation" />
          <span class="shine-effect"></span>
        </div>
      </section>

      <!-- Feature 3: Health Guardian -->
      <section class="feature-section health-section">
        <div class="feature-text">
          <h2>Your Proactive Guardian</h2>
          <h3>Predictive Health Alerts</h3>
          <p>
            Go beyond simple tracking. The SW11 uses advanced biosensors and AI algorithms to monitor your vitals 24/7. 
            It analyzes trends in heart rate variability, SpO2, and body temperature to provide early warnings for potential health risks, giving you and your loved ones peace of mind.
          </p>
        </div>
        <div class="feature-image">
           <!-- [图片占位] 请替换为你自己的图片 -->
          <img src="../assets/health-monitoring.jpg" alt="Health Monitoring and Alerts" />
        </div>
      </section>

    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';
import gsap from 'gsap';
// [新增] 引入 ScrollTrigger 插件
import { ScrollTrigger } from 'gsap/ScrollTrigger';

// [新增] 注册插件，这是必须的步骤！
gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  // --- 原有的 Hero Section 动画 (稍作调整) ---
  const tl = gsap.timeline({ defaults: { ease: 'power3.out' } });

  tl.from('.hero-text h1', { y: 50, opacity: 0, duration: 0.8 })
    .from('.hero-text p', { y: 50, opacity: 0, duration: 0.8 }, '-=0.6')
    .from('.hero-text .cta-button-main', { y: 50, opacity: 0, duration: 0.8 }, '-=0.6')
    .from('.hero-image', { opacity: 0, scale: 0.95, duration: 1.5 }, '-=0.8');

  // --- [全新] 功能区滚动触发动画 ---

  // 动画 1: AR 互动区 (左右滑入 + 视差)
  const arSection = document.querySelector('.ar-section');
  gsap.from(arSection.querySelector('.feature-text'), {
    scrollTrigger: {
      trigger: arSection,
      start: 'top 80%', // 当区域顶部进入视窗80%时
      end: 'bottom top', // 当区域底部离开视窗顶部时
      scrub: 1, // 动画与滚动条同步
    },
    x: -100, // 从左侧-100px的位置开始
    opacity: 0,
    ease: 'power2.out',
  });
  gsap.from(arSection.querySelector('.feature-image'), {
    scrollTrigger: {
      trigger: arSection,
      start: 'top 80%',
      end: 'bottom top',
      scrub: 1,
    },
    x: 100, // 从右侧+100px的位置开始
    opacity: 0,
    ease: 'power2.out',
  });

  // 动画 2: AI 翻译区 (蒙版揭示)
  const translationSection = document.querySelector('.translation-section');
  gsap.from(translationSection.querySelector('.feature-image img'), {
    scrollTrigger: {
      trigger: translationSection,
      start: 'top 75%',
      toggleActions: 'play none none reverse', // 进入时播放，离开时反向
    },
    // 使用 clip-path 实现从上到下的揭示效果
    clipPath: 'inset(100% 0% 0% 0%)',
    scale: 1.2, // 揭示时伴随轻微缩小效果
    duration: 1.2,
    ease: 'expo.out',
  });
  gsap.from(translationSection.querySelectorAll('.feature-text > *'), {
    scrollTrigger: {
      trigger: translationSection,
      start: 'top 70%',
      toggleActions: 'play none none reverse',
    },
    y: 40,
    opacity: 0,
    duration: 0.8,
    stagger: 0.2, // 文本元素逐一出现
    ease: 'power3.out',
  });
  
  // 动画 3: 健康预警区 (缩放旋转 + 背景辉光)
  const healthSection = document.querySelector('.health-section');
  // 背景辉光动画
  gsap.fromTo(healthSection, 
    { '--glow-opacity': 0, '--glow-scale': 0.5 },
    {
      scrollTrigger: {
        trigger: healthSection,
        start: 'top 80%',
        end: 'center 60%',
        scrub: 1.5,
      },
      '--glow-opacity': 0.3,
      '--glow-scale': 1,
      ease: 'sine.inOut'
    }
  );
  // 内容动画
  gsap.from(healthSection.querySelector('.feature-image'), {
    scrollTrigger: {
      trigger: healthSection,
      start: 'top 70%',
      toggleActions: 'play none none reverse',
    },
    scale: 0.8,
    opacity: 0,
    rotationZ: -10, // 带一点旋转
    duration: 1,
    ease: 'back.out(1.2)', // 带有回弹效果
  });
  gsap.from(healthSection.querySelectorAll('.feature-text > *'), {
    scrollTrigger: {
      trigger: healthSection,
      start: 'top 65%',
      toggleActions: 'play none none reverse',
    },
    x: -50,
    opacity: 0,
    duration: 0.8,
    stagger: 0.2,
    ease: 'power3.out',
  });

  initImageHoverEffects();

});

function initImageHoverEffects() {
  
  // 效果 1: AR 互动区 - 3D 倾斜效果
  const arImageContainer = document.querySelector('.ar-section .feature-image');
  const arImage = arImageContainer.querySelector('img');

  arImageContainer.addEventListener('mousemove', (e) => {
    const { left, top, width, height } = arImageContainer.getBoundingClientRect();
    const x = e.clientX - left;
    const y = e.clientY - top;

    // 将鼠标位置从 0-width/height 映射到 -1 到 1
    const mouseX = (x / width) * 2 - 1;
    const mouseY = (y / height) * 2 - 1;

    // 定义最大倾斜和移动量
    const maxTilt = 8; // 度
    const maxMove = 10; // 像素

    gsap.to(arImage, {
      duration: 0.5,
      rotationY: maxTilt * mouseX,
      rotationX: -maxTilt * mouseY,
      x: -maxMove * mouseX,
      y: -maxMove * mouseY,
      ease: 'power1.out',
    });
  });

  arImageContainer.addEventListener('mouseleave', () => {
    gsap.to(arImage, {
      duration: 0.8,
      rotationY: 0,
      rotationX: 0,
      x: 0,
      y: 0,
      ease: 'elastic.out(1, 0.5)', // 回弹效果
    });
  });

  // 效果 2: AI 翻译区 - 光泽扫过效果
  const translationImageContainer = document.querySelector('.translation-section .feature-image');
  const shineEffect = translationImageContainer.querySelector('.shine-effect');
  
  const shineTl = gsap.timeline({ paused: true });
  shineTl.fromTo(shineEffect, 
    { left: '-120%' }, // 从左侧外部开始
    { left: '120%', duration: 0.8, ease: 'power1.inOut' } // 移动到右侧外部
  );

  translationImageContainer.addEventListener('mouseenter', () => {
    shineTl.restart();
  });
  
  // 效果 3: 健康预警区 - 心跳脉冲效果
  const healthImage = document.querySelector('.health-section .feature-image img');
  const healthContainer = document.querySelector('.health-section .feature-image');
  
  const pulseTl = gsap.timeline({ paused: true, repeat: -1, yoyo: true });
  pulseTl.to(healthImage, {
    scale: 1.03,
    duration: 1.2,
    ease: 'sine.inOut',
  }).to(healthImage, {
    // 我们可以同时动画 box-shadow 来增强效果
    boxShadow: '0 25px 60px rgba(0, 217, 255, 0.4)',
    duration: 1.2,
    ease: 'sine.inOut',
  }, '<'); // '<' 表示与上一个动画同时开始

  healthContainer.addEventListener('mouseenter', () => {
    pulseTl.play();
  });

  healthContainer.addEventListener('mouseleave', () => {
    // 平滑地停止并恢复原状
    gsap.to(healthImage, {
      scale: 1,
      boxShadow: '0 20px 50px rgba(0, 0, 0, 0.4)',
      duration: 0.5,
      ease: 'power2.out',
      onComplete: () => {
        pulseTl.pause(0); // 在动画完成后重置时间线
      }
    });
  });
}

</script>

<style scoped>
/* --- 保留原有的 Hero Section 样式 --- */
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 80px 5% 40px;
  box-sizing: border-box;
}
.hero-content { flex: 1; display: flex; justify-content: center; }
.hero-text { max-width: 500px; text-align: left; }
.hero-text h1 { font-size: 4rem; font-weight: 700; line-height: 1.1; margin-bottom: 20px; text-shadow: 0 0 15px rgba(0, 217, 255, 0.4); }
.hero-text p { font-size: 1.2rem; font-weight: 300; color: var(--secondary-text-color); margin-bottom: 40px; }
.cta-button-main { display: inline-block; background-color: var(--accent-color); color: #040713; padding: 15px 35px; border-radius: 50px; text-decoration: none; font-weight: 500; font-size: 1.1rem; transition: transform 0.3s ease, box-shadow 0.3s ease; box-shadow: 0 5px 25px rgba(0, 217, 255, 0.4); }
.cta-button-main:hover { transform: translateY(-5px); box-shadow: 0 10px 35px rgba(0, 217, 255, 0.6); }
.hero-image { flex: 1; display: flex; justify-content: center; align-items: center; }
.hero-image img { max-width: 100%; max-height: 80vh; object-fit: contain; filter: drop-shadow(0 10px 30px rgba(0, 0, 0, 0.5)); }

/* --- [新增] 功能介绍区通用样式 --- */
.feature-sections-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 80px 0;
}

.feature-section {
  display: flex;
  /* [修改] 尝试将 align-items 改为 flex-start，让内容从顶部对齐 */
  align-items: flex-start;
  gap: 5%;
  padding: 100px 5%;
  margin-bottom: 80px;
  min-height: 70vh;
  position: relative; /* 为了健康区的背景辉光定位 */
  overflow: hidden; /* 防止动画元素溢出 */
}

.feature-text {
  flex: 1;
}

.feature-image {
  flex: 1;
  /* [修改] 移除 flex: 1; 让图片容器根据其内容（图片）自动调整尺寸 */
  /* flex: 1; REMOVE */

  display: flex;
  /* [修改] 确保内容在容器内居中对齐（水平和垂直） */
  justify-content: center;
  align-items: center;

  /* [新增] 为内部的 shine-effect 提供定位上下文 */
  position: relative;
}
.ar-section .feature-image img {
  /* [新增] 确保倾斜效果在3D空间中渲染 */
  transform-style: preserve-3d;
  transition: box-shadow 0.3s ease; /* 给阴影一个平滑过渡 */
}
.ar-section .feature-image:hover img {
   box-shadow: 0 30px 70px rgba(0, 0, 0, 0.5);
}
.ar-section .feature-image {
  perspective: 1000px;
}

.feature-image img {
  max-width: 100%;
  border-radius: 15px;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4);
}

.feature-text h2 {
  font-size: 2.8rem;
  font-weight: 700;
  color: var(--primary-text-color);
  margin-bottom: 10px;
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.1);
}

.feature-text h3 {
  font-size: 1.5rem;
  font-weight: 500;
  color: var(--accent-color);
  margin-bottom: 25px;
  text-shadow: 0 0 8px rgba(0, 217, 255, 0.5);
}

.feature-text p {
  font-size: 1.1rem;
  line-height: 1.8;
  color: var(--secondary-text-color);
}

/* --- 特定功能区样式 --- */



/* 布局反转 */
.layout-reverse {
  flex-direction: row-reverse;
}

/* AI 翻译区图片容器，用于clip-path */
.translation-section .feature-image {
  border-radius: 15px;
  overflow: hidden; /* 关键！隐藏被clip-path裁切的部分 */
}

/* 健康预警区背景辉光 */
.health-section {
  /* 注册CSS变量给GSAP使用 */
  --glow-opacity: 0;
  --glow-scale: 0.5;
}
.health-section::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 800px;
  height: 800px;
  background: radial-gradient(circle, rgba(0, 217, 255, 0.8) 0%, rgba(0, 217, 255, 0) 70%);
  transform: translate(-50%, -50%) scale(var(--glow-scale));
  opacity: var(--glow-opacity);
  z-index: -1;
  pointer-events: none;
}
/* [新增] 光泽扫过效果的样式 */
.shine-effect {
  position: absolute;
  top: 0;
  left: -120%; /* 初始位置在元素外左侧 */
  width: 50%; /* 光泽的宽度 */
  height: 100%;
  background: linear-gradient(
    to right,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 0.3) 50%,
    rgba(255, 255, 255, 0) 100%
  );
  transform: skewX(-25deg); /* 倾斜光泽 */
  pointer-events: none; /* 确保它不影响鼠标事件 */
}


/* [新增] 给健康区图片容器一个cursor，提示可交互 */
.health-section .feature-image {
  cursor: pointer;
}
/* --- 响应式布局调整 --- */
@media (max-width: 900px) {
  .hero-section {
    flex-direction: column;
    text-align: center;
    margin-top: 80px;
    min-height: auto;
  }
  .hero-text {
    text-align: center;
    margin-bottom: 40px;
  }
  .hero-text h1 { font-size: 3rem; }

  .feature-section, .layout-reverse {
    flex-direction: column;
    gap: 40px;
    padding: 60px 5%;
    text-align: center;
  }
  .feature-text {
     order: 2; /* 文本始终在图片下方 */
  }
  .feature-image {
     order: 1;
  }
}
</style>