<template>
  <div class="min-h-screen px-8 py-6 box-border bg-white relative">
    <!-- 顶部标题+Logo栏 -->
    <header class="flex justify-between items-center mb-6 pb-3 border-b-2 border-[#73a942]">
      <h1 class="text-2xl text-black font-bold m-0">{{ $frontmatter.titleEn }}</h1>
      <div class="g-logo">
        <img src="/scut-logo.png" alt="院校Logo" class="h-15" />
      </div>
    </header>

    <div class="g-left">
        <slot name="middle" />
    </div>
    
    <!-- 主体分栏：大屏flex不换行，小屏换行 -->
    <div class="flex gap-8 min-h-[calc(100vh-120px)] box-border lg:flex-nowrap flex-wrap">
       
      <!-- 左栏：新增滚动逻辑，和右栏完全一致 -->
      <div class="g-left 
                  lg:w-1/2 w-full               <!-- 大屏占1/2，小屏占满 -->
                  lg:min-w-[450px] min-w-0      <!-- 大屏最小宽度保护 -->
                  lg:flex-shrink-0              <!-- 禁止收缩，防挤压 -->
                  flex flex-col gap-4 text-sm   <!-- 统一布局/间距/字体 -->
                  text-gray-800 pr-2            <!-- 统一文本颜色、右侧间距 -->
                  lg:h-[calc(100vh-300px)] h-auto <!-- 大屏固定高度（滚动前提） -->
                  lg:overflow-y-auto overflow-visible <!-- 大屏滚动，小屏不滚动 -->
                  scrollbar-thin scrollbar-thumb-rounded 
                  scrollbar-track-gray-100 scrollbar-thumb-[#73a942]">
        <slot name="left" />
      </div>

      <!-- 右栏：保留原有滚动逻辑 -->
      <div class="g-right 
                  lg:w-1/2 w-full               <!-- 大屏占1/2，小屏占满 -->
                  lg:flex-shrink-0              <!-- 禁止收缩，防挤压 -->
                  lg:max-w-[450px]              <!-- 大屏右栏最大宽度，不超宽 -->
                  flex flex-col gap-4 text-sm   <!-- 和左栏统一的布局/间距/字体 -->
                  text-gray-800 pr-2            <!-- 统一文本颜色、右侧间距 -->
                  lg:h-[calc(100vh-300px)] h-auto <!-- 大屏固定高度（滚动），小屏自适应 -->
                  lg:overflow-y-auto overflow-visible <!-- 大屏滚动，小屏不滚动 -->
                  scrollbar-thin scrollbar-thumb-rounded 
                  scrollbar-track-gray-100 scrollbar-thumb-[#73a942]">
        <slot name="right" />
      </div>
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
/* 统一左右栏的标题/粗体/行高样式 */
:deep(.g-left h1),
:deep(.g-right h1) {
  font-size: 18px !important;
  color: #000;
  margin: 0 0 1rem 0 !important;
}
:deep(.g-left h2),
:deep(.g-right h2) {
  font-size: 15px !important;
  color: #000;
  margin: 1.2rem 0 0.8rem 0 !important;
}
:deep(.g-left strong),
:deep(.g-right strong) {
  color: #73a942;
}
:deep(.g-left),
:deep(.g-right) {
  line-height: 1.8 !important;
}
</style>