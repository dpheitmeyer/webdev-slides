<script setup>
import { computed } from 'vue'
import { useSlideContext } from '@slidev/client'

const { $clicks } = useSlideContext()

const showStart      = computed(() => $clicks.value >= 1)
const showEnd        = computed(() => $clicks.value >= 2)
const showMirror     = computed(() => $clicks.value >= 2)
const highlightSlash = computed(() => $clicks.value >= 3)
const showContent    = computed(() => $clicks.value >= 4)
</script>

<template>
  <div class="flex flex-col items-center gap-4 font-mono select-none">

    <!-- Wrapper: reserves space for bracket label, shows border on click 4 -->
    <div class="relative pt-8">

      <!-- Element bracket border (click 4) -->
      <div
        v-if="showContent"
        v-motion
        :initial="{ opacity: 0 }"
        :enter="{ opacity: 1, transition: { duration: 500 } }"
        class="absolute inset-x-0 top-0 bottom-0 border-t-2 border-l-2 border-r-2 border-gray-400 pointer-events-none rounded-t"
      />

      <!-- "element" label centered on top border -->
      <div
        v-if="showContent"
        v-motion
        :initial="{ opacity: 0 }"
        :enter="{ opacity: 1, transition: { duration: 500 } }"
        class="absolute top-0 left-1/2 -translate-x-1/2 -translate-y-1/2 bg-white dark:bg-[#121212] px-3 text-gray-500 text-sm whitespace-nowrap"
      >
        element
      </div>

    <!-- Main row -->
    <div class="flex items-center gap-4 text-5xl pb-4">

      <!-- Start tag flies in from left -->
      <div
        v-if="showStart"
        v-motion
        :initial="{ x: -200, opacity: 0 }"
        :enter="{ x: 0, opacity: 1, transition: { type: 'spring', stiffness: 80, damping: 14 } }"
        class="flex"
      >
        <span class="text-blue-600 dark:text-blue-400">&lt;</span>
        <span class="text-gray-800 dark:text-gray-200">h1</span>
        <span class="text-blue-600 dark:text-blue-400">&gt;</span>
      </div>

      <!-- Center: mirror line + content -->
      <div class="relative flex flex-col items-center" style="width: 12rem; height: 4rem;">
        <div
          v-if="showMirror"
          v-motion
          :initial="{ scaleY: 0, opacity: 0 }"
          :enter="{ scaleY: 1, opacity: 1, transition: { duration: 400 } }"
          class="mirror-line absolute top-0"
        />
        <div
          v-if="showContent"
          v-motion
          :initial="{ opacity: 0, y: 20 }"
          :enter="{ opacity: 1, y: 0, transition: { delay: 200, duration: 500 } }"
          class="text-green-700 dark:text-green-300  absolute  -translate-y-1/2 whitespace-nowrap"
        >
          Hello, World!
        </div>
      </div>

      <!-- End tag flies in from right -->
      <div
        v-if="showEnd"
        v-motion
        :initial="{ x: 200, opacity: 0 }"
        :enter="{ x: 0, opacity: 1, transition: { type: 'spring', stiffness: 80, damping: 14 } }"
        class="flex"
      >
        <span class="text-blue-600 dark:text-blue-400">&lt;</span>
        <span
          :class="highlightSlash ? 'text-orange-600 dark:text-orange-400' : 'text-blue-600 dark:text-blue-400'"
          class="transition-colors duration-500"
          :style="highlightSlash ? 'transform: scale(1.25); display: inline-block;' : ''"
        >/</span>
        <span class="text-gray-800 dark:text-gray-200">h1</span>
        <span class="text-blue-600 dark:text-blue-400">&gt;</span>
      </div>

    </div>
    </div><!-- end bracket wrapper -->

    <!-- "only difference" label -->
    <div
      v-if="highlightSlash"
      v-motion
      :initial="{ opacity: 0, y: 10 }"
      :enter="{ opacity: 1, y: 0, transition: { delay: 300, duration: 400 } }"
      class="text-orange-600 dark:text-orange-400 text-sm"
    >
      the only difference
    </div>

  </div>
</template>
