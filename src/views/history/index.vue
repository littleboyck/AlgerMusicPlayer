<template>
  <div class="history-page">
    <div class="title">播放历史</div>
    <n-scrollbar :size="100">
      <div class="history-list-content" :class="setAnimationClass('animate__bounceInLeft')">
        <div
          v-for="(item, index) in musicList"
          :key="item.id"
          class="history-item"
          :class="setAnimationClass('animate__bounceIn')"
          :style="setAnimationDelay(index, 30)"
        >
          <song-item class="history-item-content" :item="item" />
          <div class="history-item-count">
            {{ item.count }}
          </div>
          <div class="history-item-delete">
            <i class="iconfont icon-close" @click="delMusic(item)"></i>
          </div>
        </div>
      </div>
    </n-scrollbar>
  </div>
</template>

<script setup lang="ts">
import { useMusicHistory } from '@/hooks/MusicHistoryHook';
import { setAnimationClass, setAnimationDelay } from '@/utils';

defineOptions({
  name: 'History',
});

const { delMusic, musicList } = useMusicHistory();
</script>

<style scoped lang="scss">
.history-page {
  @apply h-full w-full pt-2;
  .title {
    @apply pl-4 text-xl font-bold;
  }

  .history-list-content {
    @apply px-4 mt-2 pb-28;
    .history-item {
      @apply flex items-center justify-between;
      &-content {
        @apply flex-1;
      }
      &-count {
        @apply px-4 text-lg;
      }
      &-delete {
        @apply cursor-pointer rounded-full border-2 border-gray-400 w-8 h-8 flex justify-center items-center;
      }
    }
  }
}
</style>
