<template>
  <!-- [新增] 技术规格区域 -->
  <div class="specs-page" id="specs">
    <div class="specs-container">
      <h2 class="specs-title">Technical Specifications</h2>

      <p class="specs-summary" v-html="highlightedSummary"></p>
      
      <div class="table-wrapper">
        <table class="specs-table">
          <thead>
            <tr>
              <th>Feature</th>
              <th v-for="model in models" :key="model.name">{{ model.name }}</th>
            </tr>
          </thead>
          <tbody>
            <template v-for="(spec, index) in specCategories" :key="spec.feature">
              <!-- Add a category header row when the category changes -->
              <tr v-if="index === 0 || spec.category !== specCategories[index - 1].category" class="category-header">
                <td :colspan="models.length + 1">{{ spec.category }}</td>
              </tr>
              <!-- Regular spec row -->
              <tr>
                <th>{{ spec.feature }}</th>
                <td v-for="(value, i) in spec.values" :key="i" v-html="value"></td>
              </tr>
            </template>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

// --- [数据] 模型名称 ---
const models = ref([
  { name: 'ECG Edition' },
  { name: 'Stainless Steel' },
  { name: '46mm Aluminum' },
  { name: '41mm Aluminum' },
]);

// --- [数据] 规格参数，已翻译和精简 ---
const specCategories = ref([
  // --- Appearance ---
  { category: 'Appearance', feature: 'Colors', values: ['Silver', 'Silver', 'Black, Gold', 'Black, Pink Gold, <br>Mist Silver, Aqua Green'] },
  { category: 'Appearance', feature: 'Case Material', values: ['316L Stainless Steel', '316L Stainless Steel', 'Aluminum Alloy', 'Aluminum Alloy'] },
  { category: 'Appearance', feature: 'Default Strap', values: ['Fluororubber', 'Italian Calfskin', 'Fluororubber', 'Fluororubber'] },
  { category: 'Appearance', feature: 'Back Cover', values: ['Ceramic + Sapphire', 'Ceramic + Sapphire', 'Ceramic + PC', 'Ceramic + PC'] },
  { category: 'Appearance', feature: 'Weight (w/o strap)', values: ['≈ 45.5g', '≈ 45.5g', '≈ 40g', '≈ 29.7g'] },
  
  // --- Display ---
  { category: 'Display', feature: 'Screen Type', values: ['AMOLED Flexible Screen', 'AMOLED Flexible Screen', 'AMOLED Flexible Screen', 'AMOLED Screen'] },
  { category: 'Display', feature: 'Screen Size', values: ['1.91 inch', '1.91 inch', '1.91 inch', '1.6 inch'] },
  
  // --- Performance & Core ---
  { category: 'Performance', feature: 'Processor', values: ['Snapdragon 2500 &<br>Apollo 3', 'Snapdragon 2500 &<br>Apollo 3', 'Snapdragon 2500 &<br>Apollo 3', 'Snapdragon 2500 &<br>Apollo 3'] },
  { category: 'Performance', feature: 'Operating System', values: ['ColorOS Watch', 'ColorOS Watch', 'ColorOS Watch', 'ColorOS Watch'] },
  { category: 'Performance', feature: 'Memory', values: ['1GB RAM + 8GB ROM', '1GB RAM + 8GB ROM', '1GB RAM + 8GB ROM', '1GB RAM + 8GB ROM'] },
  { category: 'Performance', feature: 'Battery Capacity', values: ['430mAh', '430mAh', '430mAh', '300mAh'] },
  { category: 'Performance', feature: 'Typical Usage', values: ['40 hours', '40 hours', '40 hours', '24 hours'] },
  { category: 'Performance', feature: 'Power Saver Mode', values: ['21 days', '21 days', '21 days', '14 days'] },
  { category: 'Performance', feature: 'Charging', values: ['Watch VOOC Flash Charge', 'Watch VOOC Flash Charge', 'Watch VOOC Flash Charge', 'Watch VOOC Flash Charge'] },

  // --- Health & Fitness ---
  { category: 'Health & Fitness', feature: 'Key Health Functions', values: ['<b>ECG Detection</b>,<br>Heart Rate Monitor,<br>Sleep Tracking', 'Heart Rate Monitor,<br>Sleep Tracking,<br>Menstrual Cycle', 'Heart Rate Monitor,<br>Sleep Tracking,<br>Menstrual Cycle', 'Heart Rate Monitor,<br>Sleep Tracking,<br>Menstrual Cycle'] },
  { category: 'Health & Fitness', feature: 'Water Resistance', values: ['5 ATM / IPX8', '5 ATM / IPX8', '5 ATM', '3 ATM'] },
  
  // --- Connectivity ---
  { category: 'Connectivity', feature: 'eSIM Support', values: ['Supported', 'Supported', 'Supported', 'Supported'] },
  { category: 'Connectivity', feature: 'GPS', values: ['Built-in GPS, A-GPS, BeiDou', 'Built-in GPS, A-GPS, BeiDou', 'Built-in GPS, A-GPS, BeiDou', 'Built-in GPS, A-GPS, BeiDou'] },
  { category: 'Connectivity', feature: 'NFC', values: ['Supported', 'Supported', 'Supported', 'Supported'] },
]);

// [新增] 1. 定义原始的、不带任何标签的概述文本
const summaryText = ref(
  "Fusing premium craftsmanship with potent technology, the SW11 is engineered for excellence. The robust stainless steel case frames a stunning 1.91-inch flexible AMOLED display, bringing every detail to life. At its heart, a powerful dual-engine platform featuring Qualcomm Snapdragon & Apollo processors orchestrates a seamless experience, ensuring fluid performance and remarkable battery life. With advanced features like ECG monitoring and independent eSIM connectivity, the SW11 is a truly comprehensive and powerful smart device."
);

// [新增] 2. 定义一个数组，包含所有我们想高亮的关键词
const keywordsToHighlight = [
  'stainless steel',
  '1.91-inch flexible AMOLED display',
  'dual-engine platform',
  'Qualcomm Snapdragon & Apollo processors',
  'ECG monitoring',
  'eSIM connectivity'
];

// [新增] 3. 创建一个计算属性，它会自动为关键词添加高亮样式
const highlightedSummary = computed(() => {
  let text = summaryText.value;
  // 遍历所有关键词
  keywordsToHighlight.forEach(keyword => {
    // 使用正则表达式进行全局、不区分大小写的替换
    // 将关键词用一个带 'highlight' 类的 <span> 包裹起来
    const regex = new RegExp(`(${keyword})`, 'gi');
    text = text.replace(regex, `<span class="highlight">$1</span>`);
  });
  return text;
});

onMounted(() => {
  // --- [动画] 技术规格区域入场动画 ---
  const specsTl = gsap.timeline({
    scrollTrigger: {
      trigger: '.specs-page',
      start: 'top 80%',
      toggleActions: 'play none none reverse'
    }
  });

  // 1. 标题滑入
  specsTl.from('.specs-title', {
    y: 50,
    opacity: 0,
    duration: 0.8,
    ease: 'power3.out'
  });

  // [新增] 2. 概述文本滑入
  specsTl.from('.specs-summary', {
    y: 40,
    opacity: 0,
    duration: 0.8,
    ease: 'power3.out'
  }, '-=0.6'); // 与标题动画重叠开始，效果更流畅

  // 3. 表格整体淡入
  specsTl.from('.table-wrapper', {
    opacity: 0,
    duration: 0.5
  }, '-=0.5');

  // 4. 表格的行使用 stagger 效果逐一滑入
  specsTl.from('.specs-table tr', {
    y: 20,
    opacity: 0,
    duration: 0.6,
    ease: 'power2.out',
    stagger: 0.05
  }, '-=0.3');
});
</script>

<style scoped>
.specs-page {
  padding: 120px 5%;
  background-color: rgba(0, 0, 0, 0.2); /* 给一个深色背景以区分 */
}

.specs-container {
  max-width: 1200px;
  margin: 0 auto;
}

.specs-title {
  font-size: 2.8rem;
  color: var(--accent-color);
  text-shadow: 0 0 10px rgba(0, 217, 255, 0.5);
  /* [改动] 调整标题下方的间距 */
  margin-bottom: 25px; 
  text-align: center;
}

/* [新增] 概述文本的样式 */
.specs-summary {
  max-width: 700px; /* 限制最大宽度以提高可读性 */
  margin: 0 auto 60px; /* 顶部0, 左右自动居中, 底部60px */
  text-align: center;
  font-size: 1.1rem;
  line-height: 1.7;
  color: var(--secondary-text-color);
  font-weight: 300;
}
.specs-summary :deep(.highlight) {
  color: var(--accent-color); /* 使用你的主题强调色 */
  font-weight: 600; /* 让字体更粗，更醒目 */
}

.table-wrapper {
  overflow-x: auto; /* 在小屏幕上启用水平滚动 */
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  background-color: rgba(255, 255, 255, 0.03);
}

.specs-table {
  width: 100%;
  border-collapse: collapse;
  color: var(--primary-text-color);
  font-size: 0.95rem;
  min-width: 800px; /* 保证表格在小屏幕滚动前有最小宽度 */
}

.specs-table th, .specs-table td {
  padding: 18px 15px;
  text-align: center;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  vertical-align: middle;
}

/* 表头样式 */
.specs-table thead th {
  background-color: rgba(0, 217, 255, 0.1);
  font-size: 1.1rem;
  font-weight: 500;
  color: var(--accent-color);
  position: sticky;
  top: 0; /* 如果页面可滚动，使表头置顶 */
  z-index: 10;
}
.specs-table thead th:first-child {
  text-align: left;
  background-color: transparent;
  color: var(--secondary-text-color);
}

/* 分类标题行样式 */
.category-header td {
  background-color: rgba(255, 255, 255, 0.08);
  font-weight: 600;
  font-size: 1.2rem;
  text-align: left;
  padding-left: 20px;
  color: var(--primary-text-color);
}

/* 表格主体行样式 */
.specs-table tbody tr:not(.category-header):hover {
  background-color: rgba(255, 255, 255, 0.05);
}

/* 特征列（第一列）样式 */
.specs-table tbody th {
  text-align: left;
  font-weight: 400;
  color: var(--secondary-text-color);
  width: 25%; /* 固定第一列宽度 */
}

/* 数据列样式 */
.specs-table tbody td {
  color: var(--primary-text-color);
  line-height: 1.6;
}

/* 突出显示ECG功能 */
.specs-table td :deep(b) {
  color: var(--accent-color);
  font-weight: 600;
}

@media (max-width: 900px) {
  .specs-title {
    font-size: 2.2rem;
  }
  .specs-table th, .specs-table td {
    padding: 12px 10px;
    font-size: 0.9rem;
  }
}
</style>