<template>
  <div class="support-page">
    <!-- Section 1: Service Overview -->
    <section class="service-overview">
      <div class="container">
        <h1 class="page-title">Our Commitment to You</h1>
        <p class="page-subtitle">
          Your experience with the SW11 doesn't end at purchase. We stand behind our product with a comprehensive suite of support services designed to give you peace of mind.
        </p>
        <div class="overview-grid">
          <div v-for="service in services" :key="service.title" class="service-card">
            <div class="card-icon-wrapper">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="card-icon" v-html="service.icon"></svg>
            </div>
            <h3>{{ service.title }}</h3>
            <p>{{ service.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Section 2: Detailed Policies -->
    <section class="detailed-terms">
      <div class="container">
        <h2 class="section-title">Detailed Service Policies</h2>
        <div class="accordion">
          <div v-for="(item, index) in policies" :key="index" class="accordion-item">
            <button @click="toggleAccordion(index)" class="accordion-header">
              <span>{{ item.title }}</span>
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="chevron-icon" :class="{ 'is-open': activeAccordionIndex === index }">
                <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
              </svg>
            </button>
            <div class="accordion-content-wrapper" ref="accordionContents">
              <div class="accordion-content">
                <p v-html="item.content"></p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

// --- 数据: 服务概览卡片 ---
const services = ref([
  {
    title: '1-Year Limited Warranty',
    icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75L11.25 15 15 9.75m-3-7.036A11.959 11.959 0 013.598 6 11.99 11.99 0 003 9.749c0 5.592 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.286zm0 13.036h.008v.008h-.008v-.008z" />',
    description: 'Every SW11 is covered against manufacturing defects for one full year from the date of purchase. We build it to last, and we stand by it.'
  },
  {
    title: 'Expert Technical Support',
    icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M12 18.75a6 6 0 006-6v-1.5m-6 7.5a6 6 0 01-6-6v-1.5m12 0-3-3m-6 0l-3 3m-3.75 6.75h16.5a1.5 1.5 0 001.5-1.5V6a1.5 1.5 0 00-1.5-1.5H3.75A1.5 1.5 0 002.25 6v9.75a1.5 1.5 0 001.5 1.5z" />',
    description: 'Our dedicated support team is available via live chat, email, and phone to help you with setup, troubleshooting, or any questions you may have.'
  },
  {
    title: 'Hassle-Free Repairs',
    icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M11.42 15.17L17.25 21A2.652 2.652 0 0021 17.25l-5.877-5.877M11.42 15.17l2.472-2.472a3.375 3.375 0 000-4.773L6.293 2.293a3.375 3.375 0 00-4.773 0L1.5 2.312a3.375 3.375 0 000 4.773l2.472 2.472M6.88 8.872l4.544 4.544" />',
    description: 'If your watch needs service, our streamlined process ensures a quick and transparent repair experience, whether in or out of warranty.'
  },
  {
    title: 'Community & Resources',
    icon: '<path stroke-linecap="round" stroke-linejoin="round" d="M12 6.042A8.967 8.967 0 006 3.75c-1.052 0-2.062.18-3 .512v14.25A8.987 8.987 0 016 18c2.305 0 4.408.867 6 2.292m0-14.25a8.966 8.966 0 016-2.292c1.052 0 2.062.18 3 .512v14.25A8.987 8.987 0 0018 18a8.967 8.967 0 00-6-2.292m0 0v14.25" />',
    description: 'Access our extensive online knowledge base with FAQs, tutorials, and user forums to get the most out of your SW11 smartwatch.'
  }
]);

// --- 数据: 详细政策条款 ---
const policies = ref([
  {
    title: '1. One-Year Limited Warranty Policy',
    content: `
      Your SW11 smartwatch is warranted against defects in materials and workmanship for a period of one (1) year from the date of original retail purchase. <br><br>
      <strong>What is covered:</strong> This warranty covers the watch module against functional defects that are not caused by user damage. <br><br>
      <strong>What is NOT covered:</strong> This warranty does not apply to: (a) cosmetic damage, including but not limited to scratches and dents; (b) damage caused by accident, abuse, misuse, liquid contact beyond the IP rating, or other external cause; (c) damage caused by operating the product outside the published guidelines; (d) a product that has been modified; (e) normal wear and tear or otherwise due to the normal aging of the product.
    `
  },
  {
    title: '2. Repair Service Process',
    content: `
      To initiate a repair, please contact our Technical Support team first. They will diagnose the issue and guide you through the next steps.<br><br>
      <strong>In-Warranty Repairs:</strong> If the issue is covered under our Limited Warranty, the repair will be performed at no cost to you. <br><br>
      <strong>Out-of-Warranty Repairs:</strong> For issues not covered by the warranty (e.g., a cracked screen from a drop), we will provide a detailed quote for the cost of repair. No work will be done without your approval. The estimated turnaround time for most repairs is 7-10 business days upon receiving the device.
    `
  },
  {
    title: '3. Return & Exchange Policy',
    content: `
      If you are not completely satisfied with your purchase, you may return the product for a full refund or exchange within 14 days of the delivery date. <br><br>
      <strong>Conditions for Return:</strong> The product must be in like-new condition, with no visible signs of wear, and returned in its original packaging with all included accessories. We reserve the right to refuse a return or charge a restocking fee if the product is returned in poor condition.
    `
  }
]);

// --- 逻辑: 折叠面板 (Accordion) ---
const activeAccordionIndex = ref(null);
const accordionContents = ref([]);

const toggleAccordion = (index) => {
  // 获取当前点击的content wrapper
  const currentContent = accordionContents.value[index];

  // 如果点击的是已经打开的，则关闭它
  if (activeAccordionIndex.value === index) {
    gsap.to(currentContent, { maxHeight: 0, duration: 0.4, ease: 'power2.inOut' });
    activeAccordionIndex.value = null;
  } else {
    // 关闭上一个打开的 (如果存在)
    if (activeAccordionIndex.value !== null) {
      const prevContent = accordionContents.value[activeAccordionIndex.value];
      gsap.to(prevContent, { maxHeight: 0, duration: 0.4, ease: 'power2.inOut' });
    }
    
    // 打开当前点击的
    gsap.to(currentContent, { maxHeight: currentContent.scrollHeight, duration: 0.4, ease: 'power2.inOut' });
    activeAccordionIndex.value = index;
  }
};


onMounted(() => {
  // 动画: 服务概览卡片入场
  gsap.from('.service-card', {
    scrollTrigger: {
      trigger: '.overview-grid',
      start: 'top 85%',
      // markers: true, // 开启 markers 可以帮助你看到 ScrollTrigger 的触发区域，方便调试
    },
    y: 50, // 起始 Y 位置
    opacity: 0, // 起始透明度
    duration: 0.6,
    stagger: 0.15,
    ease: 'power3.out',
    // [核心修改]: 动画结束后，移除任何可能存在的 transform 属性，让元素回到其 CSS 定义的原始状态
    clearProps: "transform, opacity",
  });

  // 动画: 详细条款区域入场
  gsap.from('.accordion-item', {
    scrollTrigger: {
      trigger: '.detailed-terms',
      start: 'top 80%',
      // markers: true,
    },
    x: -40,
    opacity: 0,
    duration: 0.7,
    stagger: 0.1,
    ease: 'power3.out',
    // 同样，这里也添加 clearProps
    clearProps: "transform, opacity",
  });
});

</script>

<style scoped>
.container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 20px;
}

.support-page {
  padding-bottom: 120px;
}

/* --- Section 1: Service Overview --- */
.service-overview {
  text-align: center;
  padding: 80px 0;
}

.page-title {
  font-size: 3rem;
  font-weight: 700;
  color: var(--primary-text-color);
  margin-bottom: 20px;
}

.page-subtitle {
  font-size: 1.1rem;
  color: var(--secondary-text-color);
  max-width: 650px;
  margin: 0 auto 60px;
  line-height: 1.7;
}

/* [核心修改] 使用 Grid 来管理布局 */
.overview-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr); /* 保持两列 */
  gap: 30px;
}

.service-card {
  
  background-color: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  padding: 30px;
  text-align: left;
  transition: transform 0.3s ease, box-shadow 0.3s ease;

  display: flex;
  flex-direction: column;
  justify-content: flex-start; /* 从顶部开始对齐内容 */
}

.service-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.card-icon-wrapper {
  background-color: rgba(0, 217, 255, 0.1);
  width: 50px;
  height: 50px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
}

.card-icon {
  width: 28px;
  height: 28px;
  color: var(--accent-color);
}

.service-card h3 {
  font-size: 1.4rem;
  color: var(--primary-text-color);
  margin-bottom: 10px;
  /* [核心修改] 移除 flex-grow: 1，让标题占据它自身的高度即可 */
  /* flex-grow: 1; REMOVE */
}

.service-card p {
  font-size: 0.95rem;
  color: var(--secondary-text-color);
  line-height: 1.6;
  /* [核心修改] 移除 flex-grow: 1，让段落占据它自身的高度即可 */
  /* flex-grow: 1; REMOVE */
}


/* --- Section 2: Detailed Policies (保持不变) --- */
.detailed-terms {
  padding: 80px 0;
}
.section-title {
  text-align: center;
  font-size: 2.5rem;
  color: var(--accent-color);
  margin-bottom: 50px;
}
.accordion-item {
  border-bottom: 1px solid rgba(255, 255, 255, 0.15);
}
.accordion-header {
  width: 100%;
  background: none;
  border: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 25px 10px;
  text-align: left;
  font-size: 1.25rem;
  color: var(--primary-text-color);
  cursor: pointer;
  transition: background-color 0.3s ease;
}
.accordion-header:hover {
  background-color: rgba(255, 255, 255, 0.03);
}
.chevron-icon {
  width: 24px;
  height: 24px;
  color: var(--secondary-text-color);
  transition: transform 0.4s ease;
  flex-shrink: 0;
}
.chevron-icon.is-open {
  transform: rotate(180deg);
  color: var(--accent-color);
}
.accordion-content-wrapper {
  max-height: 0;
  overflow: hidden;
}
.accordion-content {
  padding: 0 15px 30px;
  color: var(--secondary-text-color);
  line-height: 1.8;
}
.accordion-content :deep(strong) {
  color: var(--primary-text-color);
  font-weight: 600;
}


/* --- Responsive (响应式适配) --- */
@media (max-width: 768px) {
  .page-title {
    font-size: 2.5rem;
  }
  .section-title {
    font-size: 2rem;
  }
  .accordion-header {
    font-size: 1.1rem;
  }

  /* 在小屏幕上，让网格变为一列 */
  .overview-grid {
    grid-template-columns: 1fr;
  }
}
</style>