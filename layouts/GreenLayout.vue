<template>
  <div class="g-layout">
    <!-- 顶部标题+Logo栏 -->
    <header class="g-header">
      <h1 class="g-title">{{ $frontmatter.titleEn }}</h1>
      <div class="g-logo">
        <img src="/scut-logo.png" alt="院校Logo" />
      </div>
    </header>
    <!-- 主体内容（左右分栏） -->
    <main class="g-left">
      <slot />
    </main>
  </div>
</template>

<script setup>
// 读取frontmatter中的配置（用户在幻灯片中填写）
defineProps({
  frontmatter: {
    type: Object,
    default: () => ({})
  }
})
</script>

<style scoped>
  
/* 全局布局容器 */
.g-layout {
  min-height: 100vh;
  padding: 1.5rem 2rem;
  position: relative;
  box-sizing: border-box;
  background: #fff;
}

/* 顶部标题栏 */
.g-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.2rem;
  padding-bottom: 0.6rem;
  border-bottom: 2px solid #73a942; /* 示例中的绿色下划线 */
}
.g-title {
  font-size: 24px;
  color: #000;
  margin: 0;
  font-weight: bold;
}
.g-logo img {
  height: 60px; /* 适配院校Logo大小 */
}

/* 主体分栏 */
.g-content {
  display: flex;
  gap: 2.5rem;
  height: calc(100vh - 120px); /* 留出顶部+底部空间 */
}

/* 左侧内容区 */
.g-left {
  flex: 3;
  font-size: 16px;
  line-height: 1.8;
  color: #333;
}

:deep(.g-left h1) {
  font-size: 18px !important;
  color: #000;
  margin: 0 0 1rem 0 !important;
}
:deep(.g-left h2) {
  font-size: 22px !important;
  color: #000;
  margin: 1.2rem 0 0.8rem 0 !important;
}

:deep(.g-left strong) {
  color: #73a942;
}


/* 右侧模块区 */
.g-right {
  flex: 2; /* 右侧占比 */
  display: flex;
  flex-direction: column;
  gap: 2rem;
  font-size: 15px;
}
.g-item {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}
.g-item-icon img {
  width: 32px;
  height: 32px;
}
.g-item-title {
  font-size: 18px;
  margin: 0;
  color: #000;
}
.g-item-desc {
  line-height: 1.6;
  margin: 0;
  color: #333;
}

</style>