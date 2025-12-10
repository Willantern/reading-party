<template>
  <div class="min-h-screen px-8 py-6 box-border bg-white relative">
    <!-- 顶部标题+Logo栏 -->
    <header class="flex justify-between items-center mb-6 pb-3 border-b-2 border-[#73a942]">
      <h1 class="text-2xl text-black font-bold m-0">{{ $frontmatter.titleEn }}</h1>
      <div class="g-logo">
        <img src="/scut-logo.png" alt="院校Logo" class="h-15" />
      </div>
    </header>

    <!-- 移除原双栏，改为单栏容器 -->
    <div class="g-single-column 
                w-full max-w-none lg:max-w-[900px] mx-auto  <!-- 单栏宽度自适应，大屏最大宽度900px（原双栏总和），居中 -->
                min-w-0                                    <!-- 取消最小宽度限制，适配小屏 -->
                flex flex-col gap-4 text-sm                <!-- 保留原有布局/间距/字体 -->
                text-gray-800                              <!-- 统一文本颜色 -->
                lg:h-[calc(100vh-300px)] h-auto            <!-- 大屏固定高度（滚动），小屏自适应 -->
                lg:overflow-y-auto overflow-visible        <!-- 大屏纵向滚动，小屏不滚动 -->
                scrollbar-thin scrollbar-thumb-rounded 
                scrollbar-track-gray-100 scrollbar-thumb-[#73a942]">
      <slot name="middle" />  <!-- 复用原有middle插槽，也可替换为left/right -->
    </div>
  </div>
</template>

<script setup>
defineProps({
  frontmatter: {
    type: Object,
    default: () => ({})
  }
})
</script>

<style scoped>
/* 核心修复：文本自动换行 + 溢出处理 */
:deep(.g-single-column) {
  line-height: 1.8 !important;
  /* 1. 强制长文本换行（解决无空格英文/数字溢出） */
  word-break: break-all;
  /* 2. 英文单词内换行（更优雅的换行方式，可选） */
  word-wrap: break-word;
  /* 3. 兜底：禁止横向溢出 */
  overflow-x: hidden;
  /* 4. 确保内容不超出容器宽度 */
  max-width: 100%;
}

/* 统一标题样式 */
:deep(.g-single-column h1) {
  font-size: 18px !important;
  color: #000;
  margin: 0 0 1rem 0 !important;
}
:deep(.g-single-column h2) {
  font-size: 15px !important;
  color: #000;
  margin: 1.2rem 0 0.8rem 0 !important;
}
:deep(.g-single-column strong) {
  color: #73a942;
}
</style>