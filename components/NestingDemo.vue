<script setup>
import { computed } from 'vue'
import { useSlideContext } from '@slidev/client'

const { $clicks } = useSlideContext()

const showUlOpen  = computed(() => $clicks.value >= 1)
const showLi1     = computed(() => $clicks.value >= 2)
const showLi2     = computed(() => $clicks.value >= 3)
const showLi3     = computed(() => $clicks.value >= 4)
const showUlClose = computed(() => $clicks.value >= 5)
const showRail    = computed(() => $clicks.value >= 6)
</script>

<template>
  <div class="font-mono text-3xl relative inline-block text-left leading-relaxed">

    <!-- Purple left-rail showing ul wraps everything (click 6) -->
    <div
      v-if="showRail"
      v-motion
      :initial="{ opacity: 0, scaleY: 0 }"
      :enter="{ opacity: 1, scaleY: 1, transition: { duration: 400 } }"
      class="absolute left-0 top-0 bottom-0 border-l-4 border-purple-400"
      style="transform-origin: top left;"
    />

    <!-- <ul> -->
    <div
      v-if="showUlOpen"
      v-motion
      :initial="{ opacity: 0, x: -20 }"
      :enter="{ opacity: 1, x: 0, transition: { duration: 300 } }"
      class="pl-4"
    >
      <span class="text-purple-500">&lt;ul&gt;</span>
    </div>

    <!-- <li>water</li> -->
    <div
      v-if="showLi1"
      v-motion
      :initial="{ opacity: 0, x: -20 }"
      :enter="{ opacity: 1, x: 0, transition: { duration: 300 } }"
      class="pl-12"
    >
      <span class="text-blue-600 dark:text-blue-400">&lt;li&gt;</span><!--
      --><span class="text-gray-800 dark:text-gray-200">water</span><!--
      --><span class="text-blue-600 dark:text-blue-400">&lt;/li&gt;</span>
    </div>

    <!-- <li>tea</li> -->
    <div
      v-if="showLi2"
      v-motion
      :initial="{ opacity: 0, x: -20 }"
      :enter="{ opacity: 1, x: 0, transition: { duration: 300 } }"
      class="pl-12"
    >
      <span class="text-blue-600 dark:text-blue-400">&lt;li&gt;</span><!--
      --><span class="text-gray-800 dark:text-gray-200">tea</span><!--
      --><span class="text-blue-600 dark:text-blue-400">&lt;/li&gt;</span>
    </div>

    <!-- <li>coffee</li> -->
    <div
      v-if="showLi3"
      v-motion
      :initial="{ opacity: 0, x: -20 }"
      :enter="{ opacity: 1, x: 0, transition: { duration: 300 } }"
      class="pl-12"
    >
      <span class="text-blue-600 dark:text-blue-400">&lt;li&gt;</span><!--
      --><span class="text-gray-800 dark:text-gray-200">coffee</span><!--
      --><span class="text-blue-600 dark:text-blue-400">&lt;/li&gt;</span>
    </div>

    <!-- </ul> -->
    <div
      v-if="showUlClose"
      v-motion
      :initial="{ opacity: 0, x: -20 }"
      :enter="{ opacity: 1, x: 0, transition: { duration: 300 } }"
      class="pl-4"
    >
      <span class="text-purple-500">&lt;/ul&gt;</span>
    </div>

  </div>
</template>
