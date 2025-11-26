<script setup lang="ts">
import { useNav } from '@slidev/client'

const { currentPage, total } = useNav()
</script>

<template>
  <div class="w-full h-full">
    <!-- ここにスライド本体がレンダリングされる -->
    <slot />

    <!-- 右下のページ番号 -->
    <div class="fixed bottom-4 right-6 text-sm opacity-70">
      {{ currentPage }} / {{ total }}
    </div>
  </div>
</template>
