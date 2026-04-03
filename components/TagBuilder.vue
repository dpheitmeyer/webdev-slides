<script setup>
import { computed } from 'vue'
import { useSlideContext } from '@slidev/client'

const props = defineProps({
  closing: { type: Boolean, default: false },
  tagName: { type: String, default: 'h1' },
  startAt: { type: Number, default: 1 },
})

const { $clicks } = useSlideContext()

const showOpen  = computed(() => $clicks.value >= props.startAt)
const showSlash = computed(() => props.closing && $clicks.value >= props.startAt + 1)
const showName  = computed(() => $clicks.value >= props.startAt + (props.closing ? 2 : 1))
const showClose = computed(() => $clicks.value >= props.startAt + (props.closing ? 3 : 2))
</script>

<template>
  <div class="tag-builder font-mono text-6xl flex items-center gap-1 select-none justify-center">
    <span
      v-if="showOpen"
      v-motion
      :initial="{ x: -40, opacity: 0 }"
      :enter="{ x: 0, opacity: 1, transition: { duration: 400 } }"
      class="text-blue-600 dark:text-blue-400"
    >&lt;</span>

    <span
      v-if="showSlash"
      v-motion
      :initial="{ y: -40, opacity: 0 }"
      :enter="{ y: 0, opacity: 1, transition: { duration: 400 } }"
      class="text-orange-600 dark:text-orange-400 font-bold"
    >/</span>

    <span
      v-if="showName"
      v-motion
      :initial="{ y: 30, opacity: 0 }"
      :enter="{ y: 0, opacity: 1, transition: { duration: 400 } }"
      class="text-gray-800 dark:text-gray-200"
    >{{ tagName }}</span>

    <span
      v-if="showClose"
      v-motion
      :initial="{ x: 40, opacity: 0 }"
      :enter="{ x: 0, opacity: 1, transition: { duration: 400 } }"
      class="text-blue-600 dark:text-blue-400"
    >&gt;</span>
  </div>
</template>
